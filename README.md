# Jenkins-overview
This repo contains the information about the Jenkins.
Jenkins is all about picking up the code from local or any version control system and delivering it to any environment and automating all the steps which fall in between. It acts as an orchestrator.

# Steps
1. Create an ubuntu EC2 instance on aws and then install jenkins on that.
2. Jenkins is a java based application so we need to have java(jdk) as pre-requisite.
3. So, first install jdk on ubuntu instance by opening ubuntu on the terminal.
   Run the following commands on the ec2 to install and verify jdk:
     sudo apt update
     sudo apt install openjdk-11-jre
     java --version
4. Now install jenkins on ubuntu instance. Run the following command:
     curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

5. By default, Jenkins is not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules by going to security group of that instance.
6. Open the jenkins using : 
   http://<public-ip-adress-of-ec2-instance>:8080
7. To login to jenkins, run the following command in the terminal to get the password of your account:
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword
8. Click on install suggested plugins. And then create First Admin User by giving username and password details.
    Jenkins is successfully installed.
10. Now to configure docker, install docker on same ec2. (you can install it on different machine also, just have to configure that machine as slave.
      Run the following commands:
      sudo apt update
      sudo apt install docker.io
11. Docker runs on daemon process. and by default daemon is not accessible to other user. So grant Jenkins user and Ubuntu user permission to docker deamon.
     Run the following commands:
      sudo su -  (to switch to root user as docker is installed on root : sudo apt install docker.io)
      usermod -aG docker jenkins
      usermod -aG docker ubuntu
    <Docker is the group created at the time of docker installation; we are making jenkins and ubuntu part of docker group>
       Now restart the docker daemon  -> systemctl restart docker
12. Switch to jenkins user. Jenkins user is already created when you install jenkins  -> su - jenkins
13. Verify if docker is configured with jenkins.
      docker run hello-world   <jenkins is now able to create containers>
14. Now restart the jenkins.
15. Now install the docker pluggins in jenkins so that jenkins will execute the pipelines on docker agents if the req. configuration is provided in jenkins file.
    
    Log in to Jenkins.
    Go to Manage Jenkins > Manage Plugins.
    In the Available tab, search for "Docker Pipeline".
    Select the plugin and click the Install button.
    Restart Jenkins after the plugin is installed.

16. Now click on the new item and start writing jenkin pipeline. Jenkins provide you different methods to run pipeline. Here I am using pipeline approach which is declarative and scripted pipeline.
17. Pipelines are wrttien in groovy scripting. Here you have to provide different stage and steps involved with those stages. And you can create PR to github for these pipelines. 
18. 
          
