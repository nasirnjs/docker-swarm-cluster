
MySQL Data Persistent in Docker Swarm via NFS

**Prerequisites:**

1. **Install NFS Server:** Ensure that you have installed and configured an NFS server. You can refer to [this example](https://github.com/nasirnjs/k8s-cluster-setup/blob/main/dynamic-nfs-provisioning_k8s.md) for setting up an NFS server.

2. **Reachability:** Make sure the NFS server is reachable from both the Docker Swarm master and worker nodes. You can test reachability using tools like `ping` or `telnet`.

3. **Install nfs-common:** Install the `nfs-common` package on all nodes (both master and worker nodes) where you want to mount NFS shares. This package provides the NFS client utilities needed to mount NFS shares.

4. **Mount NFS Shares (Optional):** Ensure that you have configured the Docker Swarm nodes to mount NFS shares. You can manually mount NFS shares using the `mount` command or add entries to `/etc/fstab` for automatic mounting at boot time.

**Note:** Ensure that NFS shares are exported with appropriate permissions and access controls to allow Docker Swarm nodes to mount them.

### Steps1: Setup  NFS Provisioning for Docker Swarm Cluster

First lets install NFS server on the host machine
```bash
sudo apt update
sudo apt install nfs-kernel-server -y
```
Create a directory where our NFS server will serve the files.
```bash
sudo mkdir -p /var/k8-nfs/data
sudo chown -R nobody:nogroup /var/k8-nfs/data
sudo chmod 2770 /var/k8-nfs/data
```

Add NFS export options
```bash
sudo vi /etc/exports	
/var/k8-nfs/data 172.17.18.0/24(rw,sync,no_subtree_check,no_root_squash,no_all_squash)
```

Makes the specified directories available for NFS clients to access and restart the NFS Service
```
sudo exportfs -avr
sudo systemctl restart nfs-kernel-server
sudo systemctl status nfs-kernel-server
```

On the worker and master nodes, install nfs-common package using following
`sudo apt install nfs-common -y`


### Steps2: create My-SQL Stack as uses NFS Server for Persist Volume

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


### Steps3(Optional): create My-SQL Stack with `secret` as usr NFS Server for Persist Volume

Create Secret for MySQL
`echo "Asdf1234" | docker secret create mysql_root_password -`

```
version: '3.8'

services:
  mysql:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD_FILE: /run/secrets/mysql_root_password
    secrets:
      - mysql_root_password
    deploy:
      replicas: 1
      placement:
        constraints:
          - node.role == manager
      restart_policy:
        condition: on-failure
    volumes:
      - mysql_data:/var/lib/mysql

secrets:
  mysql_root_password:
    external: true

volumes:
  mysql_data:
    driver: local
    driver_opts:
      type: nfs
      o: addr=172.17.18.120,rw
      device: ":/var/k8-nfs/data"
```
`docker stack deploy -c mysql-sec.yaml mysql-stack`