
Make monitoring directory and keep scrape and stack both both file in same directory. 

```bash
└── monitoring
    ├── prometheus-scrape.yml
    ├── promethous-stack.yaml
    └── README.md
```
First create a network.\
`docker network create --driver=overlay monitoring`

Then run Stack.\
`docker stack deploy -c prometheus-stack.yml promethous`


CPU uses query
==============
100 - (avg(irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)

Memory Query
============
(node_memory_MemTotal_bytes - node_memory_MemFree_bytes - node_memory_Buffers_bytes - node_memory_Cached_bytes) / node_memory_MemTotal_bytes * 100

Network Query
=============
irate(node_network_receive_bytes_total[5m])


Cadvisor exporter
=================
14282

Node Exporter
=============
1860

