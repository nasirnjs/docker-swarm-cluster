To create a MySQL stack in Docker Swarm using a Docker Compose file, you can define a service for MySQL in a Docker Compose file and then deploy it to your Swarm cluster. Here's an example Docker Compose file for creating a MySQL stack.

## Docker Swarm Persistent Storage with Local Storage

`vim mysql-stck.yaml`

```bash
version: '3.8'
services:
  mysql:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: Asdf1234
      MYSQL_DATABASE: mydb
      MYSQL_USER: myuser
      MYSQL_PASSWORD: Asdf1234
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql
    deploy:
      replicas: 2
volumes:
  mysql_data:
    driver: local
```
Deploy this updated stack using the docker stack deploy command.\
`docker stack deploy -c mysql-stck.yaml mysql-stack`

Check Docker service.\
`docker service ls`

Get the container ID by using docker ps on the node where the task is running.\
`docker ps | grep mysql-stack_mysql`

Exect into Container.\
`docker exec -it 233887de3a81 bash`

Login to Mysql Container using define pass.\
`bash-4.4# mysql -u root -p`

Remove the stack: Use the docker stack rm command to remove the stack.\
`docker stack rm mysql-stack`

Determine the volume Name.\
`docker volume ls`

Delete the volume: After removing the stack, you can delete the associated volume.\
`docker volume rm mysql-stack_mysql_data`

---

## Docker Swarm Persistent Storage with NFS

**Prerequisites:**

1. **Install NFS Server:** Ensure that you have installed and configured an NFS server. You can refer to [this example](https://github.com/nasirnjs/k8s-cluster-setup/blob/main/dynamic-nfs-provisioning_k8s.md) for setting up an NFS server.

2. **Reachability:** Make sure the NFS server is reachable from both the Docker Swarm master and worker nodes. You can test reachability using tools like `ping` or `telnet`.

3. **Install nfs-common:** Install the `nfs-common` package on all nodes (both master and worker nodes) where you want to mount NFS shares. This package provides the NFS client utilities needed to mount NFS shares.

4. **Mount NFS Shares (Optional):** Ensure that you have configured the Docker Swarm nodes to mount NFS shares. You can manually mount NFS shares using the `mount` command or add entries to `/etc/fstab` for automatic mounting at boot time.

**Note:** Ensure that NFS shares are exported with appropriate permissions and access controls to allow Docker Swarm nodes to mount them.


`vim mysql-pvc-stack.yaml`
```bash
version: '3.8'
services:
  mysql:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: Asdf1234
      MYSQL_DATABASE: mydb
      MYSQL_USER: myuser
      MYSQL_PASSWORD: Asdf1234
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql
    deploy:
      replicas: 2
volumes:
  mysql_data:
    driver: local
    driver_opts:
      type: nfs
      o: addr=172.17.18.120,rw
      device: ":/var/k8-nfs/data"
```

`docker stack deploy -c mysql-pvc-stack.yaml mysql-stack`

Inspect Docker volume with volume name, `docker volume ls` then inspect the volume.\
`docker volume inspect  mysql-stack_mysql_data`

