My incoming task is about pre/post process of data. Reference: [Seldon](https://docs.seldon.io/projects/seldon-core/en/latest/examples/transformers-v2-protocol.html), [KServe](https://kserve.github.io/website/0.9/modelserving/v1beta1/transformer/feast/). The key issue is how to make it decoupling from other component and easy to use. In general, pre-process need an interface which can transform data into standard form from any other non-standard data.
```flow
s=>start: 开始
e=>end: 结束
o=>operation: 操作项
s-o-e
```
## SELDON
