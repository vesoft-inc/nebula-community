# Project Ideas for Google Summer of Code 2022

NebulaGraph is applying for the Google Summer of Code 2022 project for the first time. If you are interested in working with NebulaGraph, below are some project ideas.

If you have any questions getting started, please join the [GSoC Slack channel](https://nebulagraph.slack.com/archives/C032VPK1PJB) (preferred) or send an email via devrel[at]vesoft.com

All the potential mentors of the project ideas below can be found in the Slack channel mentioned above. Feel free to DM them if you have any questions to get started.

---

## Idea: Graph workload analysis and replay

This project aims to analyze real life property graph workload to understand the pattern of graph queries. Based on the trace, create high performant graph database benchmark or trace replayer. Create multiple workload scenarios to mimic real life graph DB workload.

The expected outcomes of the project:
- Report of real life graph workload analysis
- Real life graph benchmark
- Enrich benchmark scenarios

Skills required:
- Proficient in programming
- Problem analysis and solving
- Understanding in database

**Possible mentor:** Hao Wen

**Expected size of project:** 3 months, can be extended for paper writing

**Difficulty:** Medium


## Idea: Graph database caching acceleration in cloud

We run graph database in cloud and use caching mechanism to accelerate I/O access to cloud storage, e.g., Amazon EBS, S3, etc. To further accelerate I/O access performance and improve system stability, we need to develop cache warmup mechanism for graph database in the cloud. There are potentially several solutions and each one has its own challenges in both technology and billing, e.g., data to warmup, architecture, integration with RocksDB, billing to users and cloud administrator, etc. In another word, different caching warmup solutions will directly impact our system performance and revenue.

The expected outcomes of the project:
- Design caching warmup algorithms and systems for graph database in cloud
- Develop a runnable caching warmup system in cloud

Skills required:
- Proficient in programming
- Understanding in cloud and distributed system

**Possible mentor:** Hao Wen

**Expected size of project:** 3 months, expect long time cooperation

**Difficulty:** Hard


## Idea: Optimization of multi-hop query in NebulaGraph

NebulaGraph persists an edge as key-value pair in RocksDB. If we need to make a multi-hop query, i.e. get all the followers of my followers, the query layer need to collect all result from storage layer to retrieve all my followers first, and then set them as source and call RPC of storage layer again to retrieve the followers of followers. This is a typical graph breadth-first search (BFS) algorithm, which brings huge network and serialization costs. What we need to do is save the graph topology into the same node by adding an extra node as raft learner, so the traversal of graph could be queried in that node without extra costs.

Expected outcomes of the project:
- Support the common queries (openCypher and nGQL) in NebulaGraph by traversing the graph in the topology node

This project has been initially verified and there will be a great performance improvement.

Skills required:
- Familiar with modern c++
- Have a basic understanding of graph database and the Raft protocol

**Possible mentor:** Yujue Wang

**Expected size of project:** 3 months

**Difficulty:** Hard


## Idea: Large graph 3d visualization

This project aims to enable users to view over billions of vertices and edges in 3d mode with force-directed layout on web.

Expected outcomes:
- Zoom-in to view every vertex in scene just like google earth
- Zoom-out to overview the graph space's structure by data aggregation (vertices & edges)
- Use force-directed layout to make great visual effects 

Skills required:
- Graph algorithm
- WebGL
- Golang
- Typescript
- Database

**Possible mentor:** Zhuang Miao

**Expected size of project:** 250 hours

**Difficulty:** Hard

**References:**
1. Efficient aggregation for graph summarization: https://pages.cs.wisc.edu/~jignesh/publ/summarization.pdf
2. ForceAtlas2 layout: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0098679
3. OpenOrd layout:https://www.researchgate.net/publication/253087985_OpenOrd_An_Open-Source_Toolbox_for_Large_Graph_Layout
4. d3-force-3d: https://github.com/vasturiano/d3-force-3d/blob/master/src/manyBody.js#L85
