## Key Challenges
- The machine learning or the statistic issues.
- Software engine issues.

### 1. Concept drift and data drift
How has the data changed? When data changes, sometimes it is a **gradual change**, sometimes data changes very suddenly where there's a sudden shock to a system. (`x` changes)
The term concept drift refers to if the desired mapping, from `x` to `y` changes.(`x` mapping to `y` changes)
### 2. Software engineering issues
Checklist of questions:
- Do you need **real time** predictions or **batch predictions**?
- Does your prediction service run into clouds or does it run at the edge or in a web browser?
- How much computer resources you have.
- What about the latency and throughput(such as QPS)?
- You need to log as much of the data as possible.
- Security and privacy.