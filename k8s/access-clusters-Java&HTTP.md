---
description: create a deployment on k8s with java
---
> I already have a k8s cluster on my mac, I am trying to deploy one of my docker imgae(xgboost-serving) to it. This is my first step to accomplish this target. That is creating a deployment with remote image by `ymal` file. It is a simple example of how to deal with k8s using Java.
# Part I
reference: [https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)
## Access Clusters Using the Kubernetes API
To access a cluster, you need to know the location of the cluster and have credentials to access it. With this command:
```
kubectl config view
```
there are two ways to access clusters: with or without proxy. Run kubectl in proxy mode is recommended, but I am going to do it without proxy.
It is possible to avoid using kubectl proxy by ***passing an authentication token directly to the API server.*** (that's how we access clusters with Java code)
```shell
# Check all possible clusters, as your .KUBECONFIG may have multiple contexts:
kubectl config view -o jsonpath='{"Cluster name\tServer\n"}{range .clusters[*]}{.name}{"\t"}{.cluster.server}{"\n"}{end}'

# Select name of cluster you want to interact with from above output:
# In my case, the name is "minikube"
export CLUSTER_NAME="some_server_name"

# Point to the API server referring the cluster name
APISERVER=$(kubectl config view -o jsonpath="{.clusters[?(@.name==\"$CLUSTER_NAME\")].cluster.server}")

# Create a secret to hold a token for the default service account
kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: default-token
  annotations:
    kubernetes.io/service-account.name: default
type: kubernetes.io/service-account-token
EOF

# Wait for the token controller to populate the secret with a token:
while ! kubectl describe secret default-token | grep -E '^token' >/dev/null; do
  echo "waiting for token..." >&2
  sleep 1
done

# Get the token value(decode)
TOKEN=$(kubectl get secret default-token -o jsonpath='{.data.token}' | base64 --decode)

# Explore the API with TOKEN
curl -X GET $APISERVER/api --header "Authorization: Bearer $TOKEN" --insecure
```
After creating a secret to hold a token for the default service account, we can get a token, which is our authorization. And, we also have the apiserver address, we can use them to access cluster with HTTP request.
```shell
echo $TOKEN
echo $APISERVER
```
# PART II
we can use some HTTP tools like `org.springframework.http` to create an HTTP request.
```java
public String get() {
    try {
        HttpHeaders headers = new HttpHeaders();
        headers.add("Authorization", "Bearer " + TOKEN);
        headers.add("Accept", "application/json");
        headers.add("Content-Type", "application/json");
        ResponseEntity<String> response = restTemplate.exchange(
                APISERVER + url,
                HttpMethod.GET,
                new HttpEntity<String>(headers),
                String.class);
        System.out.println("rest create resp:" + response.toString());
        return response.getBody();
    } catch (HttpClientErrorException e) {
        throw e;
    } catch (Exception e) {
        System.err.println("rest create error:"+e);
        throw e;
    }
}
```
> NOTE: The full HTTP address is `APISERVER+url`, the `url` are someting like:
> * /apis/apps/v1/namespaces/default/deployments
> * /apis/apps/v1/namespaces/default/pods

Besides, more configure is needed:
```java
static void trustAllHttpsCertificates() throws Exception {
        javax.net.ssl.TrustManager[] trustAllCerts = new javax.net.ssl.TrustManager[1];
        javax.net.ssl.TrustManager tm = new miTM();
        trustAllCerts[0] = tm;
        javax.net.ssl.SSLContext sc = javax.net.ssl.SSLContext
                .getInstance("SSL");
        sc.init(null, trustAllCerts, null);
        javax.net.ssl.HttpsURLConnection.setDefaultSSLSocketFactory(sc
                .getSocketFactory());
    }

static class miTM implements javax.net.ssl.TrustManager,
        javax.net.ssl.X509TrustManager {
    public java.security.cert.X509Certificate[] getAcceptedIssuers() {
        return null;
    }

    public boolean isServerTrusted(
            java.security.cert.X509Certificate[] certs) {
        return true;
    }

    public boolean isClientTrusted(
            java.security.cert.X509Certificate[] certs) {
        return true;
    }

    public void checkServerTrusted(
            java.security.cert.X509Certificate[] certs, String authType)
            throws java.security.cert.CertificateException {
        return;
    }

    public void checkClientTrusted(
            java.security.cert.X509Certificate[] certs, String authType)
            throws java.security.cert.CertificateException {
        return;
    }
}
```
And these must be done before you run `get()`, it is all about security.
```java
HostnameVerifier hv = (urlHostName, session) -> true;
trustAllHttpsCertificates();
HttpsURLConnection.setDefaultHostnameVerifier(hv);
```