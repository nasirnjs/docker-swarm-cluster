Install Portainer CE with Docker Swarm on Linux

[Reference](https://docs.portainer.io/start/install-ce/server/swarm/linux)

First, retrieve the stack YML manifest.\
`curl -L https://downloads.portainer.io/ce2-19/portainer-agent-stack.yml -o portainer-agent-stack.yml`

Then use the downloaded YML manifest to deploy your stack.\
`docker stack deploy -c portainer-agent-stack.yml portainer`

`docker ps`

Logging In, Now that the installation is complete, you can log into your Portainer Server instance by opening a web browser and going to.\
`https://localhost:9443`