Manage sensitive data with Docker secrets


### Create My-SQL Stack with `secret` 
**About secrets:**\
In terms of Docker Swarm services, a secret is a blob of data, such as a password, SSH private key, SSL certificate, or another piece of data that should not be transmitted over a network or stored unencrypted in a Dockerfile or in your application's source code. You can use Docker secrets to centrally manage this data and securely transmit it to only those containers that need access to it. Secrets are encrypted during transit and at rest in a Docker swarm. A given secret is only accessible to those services which have been granted explicit access to it, and only while those service tasks are running.

Create Secret for MySQL.\
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

To list all secrets in a Docker Swarm cluster.\
`docker secret ls`

Now exect to mysql docker container and login to MySQL with secret.

List the services in your stack to identify the name of the service.\
`docker stack services mysql-stack`

Service name is mysql and you want to scale it to 5 replicas.\
`docker service scale mysql-stack_mysql=5`

