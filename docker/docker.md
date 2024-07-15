

## Introduction to Docker, and Docker Swarm

---

In this part of the guide, we explore the fundamental concepts of Docker, focusing on containerization and the creation of lightweight, portable containers. We also delve into Docker Swarm, a clustering and scheduling tool for Docker containers, enabling the management of multiple containers across multiple host machines.

### Docker
- **Definition:** Understand Docker and its role in containerization, allowing applications to be packaged with dependencies into lightweight, portable containers.
- **Resource:** [Docker Documentation](https://docs.docker.com)

### Docker Swarm
- **Overview:** Learn about Docker Swarm, a clustering and scheduling tool for Docker containers, enabling the management of multiple containers across multiple host machines.
- **Resource:** [Docker Swarm Documentation](https://docs.docker.com/engine/swarm)

### Docker Machine
- **Concept:** Explore Docker Machine, a tool that enables the creation of Docker hosts on local or cloud providers, facilitating the setup of Docker Swarm clusters.
- **Resource:** [Docker Machine Documentation](https://docs.docker.com/machine)

### Installation

**Step 1 :**  Create Docker machines (to act as nodes for Docker Swarm) 
  - Create one machine as manager and others as workers
  
    - In Case of Using hyperv

    > docker-machine create --driver hyperv manager1

    - In Case of Using hyperv

    > docker-machine create --driver virtualbox manager1

**Step 2 :** Check machine created successfully
  - List Down Docker Machines
    > docker-machine ls
  - Get IP of manager machine
    > docker-machine ip manager1

**Step 3 :** SSH (connect) to docker machine
  - SSH into manager machine
      >   docker-machine ssh manager1

**Step 4 :** Initialize Docker Swarm 
   > docker swarm init --advertise-addr MANAGER_IP
  - List Nodes
    > docker node ls
    
  (this command will work only in swarm manager and not in worker)

**Step 5 :** Join workers in the swarm
    - Get command for joining as worker, So in manager node run command
       ```
        docker swarm join-token worker
      
  - This will give command to join swarm as worker

    ```
    docker swarm join-token manager

  - To Join as worker,

      ```
      1. SSH into worker node (machine) and run command to join swarm as worker

      2. In Manager Run command - docker node ls to verify worker is registered and is ready

      3. Do this for all worker machines

**Step 6 :**  On manager run standard docker commands 
   
    docker info
  
- check the swarm section, no of manager, nodes etc
 
- Now check docker swarm command options

      docker swarm

**Step 7 :**  Run containers on Docker Swarm
      
    docker service create --replicas 3 -p 80:80 --name serviceName nginx

- Check the status:

      docker service ls

      docker service ps serviceName

- Check the service running on all nodes
- Check on the browser by giving ip for all nodes

**Step 8 :** Scale service up and down On manager node

    docker service scale serviceName=2

- Inspecting Nodes (this command can run only on manager node)

      docker node inspect nodename
  
      docker node inspect self
    
      docker node inspect worker1

**Step 9 :** Shutdown node

    docker node update --availability drain worker1

**Step 10 :** Update service

    docker service update --image imagename:version web

    docker service update --image nginx:1.14.0 serviceName

**Step 11 :** Remove service
  
    docker service rm serviceName

    docker swarm leave : to leave the swarm
- Stop Docker Machine 

      docker-machine stop machineName : to stop the machine
      
      docker-machine rm machineName : to remove the machine


### Additional Resources
- **GitHub Repository:** [Your GitHub Repo](https://github.com/Mekmun-Sopheaktra)
- **Contact:** Telegram - [Mekmun_Sopheaktra](https://t.me/Mekmun_Sopheaktra)

---
