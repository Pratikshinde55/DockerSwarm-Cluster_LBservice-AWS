# DockerSwarm


🌟Docker Swarm on AWS Cloud🌟
      Swarm is Docker tool used to create Cluster,Docker Swarm mode is built into the Docker
      Engine.           

     Docker swarm have two types of nodes :
     1.Master node / Controller npde
     2.Worker node / Slaves node 

☀️Creating four nodes Swarm cluster☀️
   In this practical Creating Docker cluster , we take four AWS insatnce one of that instane make   
   Master node & remaining nodes make worker node.

   ![Screenshot 2024-02-15 154046](https://github.com/Pratikshinde55/DockerSwarm/assets/145910708/454417b7-ce3e-4def-b8c0-d9aaede85827)


Prerequisite:
   AWS account & Ec2 instance knowledge
   In all four instances install docker and start service

       #yum install docker -y
       #systemctl start docker
       #docker info <<- show Docker swarm Active or not

🏷️Step 1-
  Make one node master node ,the node which want to make master that node Ip address is required
  in my case i want make master node IP of that instance 172.31.37.180 .
  Note:To check IP use "ifconfig" command , use eth0 IP to make Swarm cluster 
   
  Docker swarm init command is used to make cluster


      #docker swarm init  --advertise-addr 172.31.37.180

      ![Screenshot 2024-02-15 155752](https://github.com/Pratikshinde55/DockerSwarm/assets/145910708/fa8dafd9-f4f1-4983-85ec-88d8fca9f3c2)


    🔔Here get one Token that paste in remaining instance that want to be make worker node

🏷️Step 2-
     Paste token in three instance (docker must be installed & service start)
           


🏷️Step 3-
      Here Docker Swarm cluster is created to check use "docker info", om master node 

          #docker node ls
           ![Screenshot 2024-02-15 162810](https://github.com/Pratikshinde55/DockerSwarm/assets/145910708/36a28ee3-7c56-4bac-bc12-55e1abd726f8)


⭐Why use Docker swarm ❓
    Swarm master node keep watching on Container or Task ,if any Container goes down for any reason
    or Fault occurs , Master node auto-matically create same task on any Node.This is known a"fault
    tolerance".
   
                          💫Load balancer & Scaling on Docker Swarm 💫

⚡Replication:
    Swarm cluster give capability to make exact copy of task in another node this concept is called 
    as Replication.

💥Load Balancer:
    Docker swarm give pre-created set-up of load balancer, In docker Swarm 'Load balancer'term is
    "Service".
     "Load Balancer=Service"
        
    Docker service (Load Balancer) is by default isolated ,It can't connect outside world it only 
    connect to Cluster nodes, But if we want to make connection to outside world , we use
    "--publish",patting,expose.

🌟Scaling :
    There are two types of Scaling Vertical scaling and Horizontal scaling,We use Horizontal 
    scaling.
    Adding more containers or instance are called as 'Scale-out'& removing Containers
    or instances is called 'scale-in'.

     🔔To start any service in cluster we use 'Master node',The master node tracks the status of 
       tasks & monitors the health of the cluster.

🏷️Steps -
 On Master node:(To start service'Load balancer)

    #docker service create --name myweb55 --publish 8080:80 vimal13/apache-webserver-php


        screnshot------
      #docker service ls <<--- Check service ls
      #docker service ps myweb55 <<-- this show where Task lauch

      For scale-out


      #docker service scale myweb55=5

      For scale-in

      #docker service scale myweb55=1

❄️check on Google/Browser
   Public IP of master instance + port no.(http://13.201.15.80:8080/)

          screnshot.....
    
    
