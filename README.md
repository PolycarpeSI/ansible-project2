1- As servers are created using terraform there is a need to track configuration done on them in an 
     automated way. Ansible is brought to the team as a configuration management tool for the job.
     
     various playbooks , roles ,plugins, collections, modules and more will be developped.
  ***Problem:   There is a problem of tracking who is adding what or changing what in those ansible codes/playbooks . 
     Propose a best practice to help track changes and reviews those changes before we deploy it to the 
     ansible server. ( github ) 
     
2- create a pipeline in jenkins that will help deploy the ansible playbook automatically create a zip file 
     with all the code , store it in jfrog and deliver those files to the ansible server on 
     the path /home/ec2-user/ansible-dev

 3- every month, we need to run yum update -y or apt update -y on all the servers.
     we need to automate this task to run every month automatically.
     4- we need jenkins to execute the playbook instead of someone login into the ansible server and execute those playbook
     How can we make that happen?

5- Each time a qa server is deployed using terraform, we need to configure the server. it is done thru
     a shell script and you need to change it to  use a playbook
     go ahead and write the playbook  for that. below is the script used.
     #!/bin/bash
     yum install lsof wget passwd docker unzip -y
     yum install java-11* -y
     mkdir -p /opt/qa/spg
     touch  /opt/qa/spg/spg.log
     systemctl start docker
     systemctl enable docker 
     
6- these are the steps used by the qa team on the qa server built in question 5 to deploy the spring boot app ( java jar file)
     
     - Delete old artifact:  rm -rf /opt/qa/spg/*.jar
     - Check if an app is running on port 8082: lsof -i :8082  ( identify the process id and kill it )
     - download the new artifact from nexus to /opt/qa/spg folder: wget --username admin --passowrd devops http://198.58.119.40:8081/repository/prof-repo/bioMedical-0.0.6-SNAPSHOT.jar  ( the version of artifact can change )
     - Bring up the app in the background: nohup java -jar /opt/qa/spg/*.jar > /opt/qa/spg.log 2>&1 &
     Go ahead and write a playbook to automate this manual process.
     
7- meeting with monitoring team to understand the process and set up automations for it.
     d