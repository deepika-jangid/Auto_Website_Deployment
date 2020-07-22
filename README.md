# Problem Statement
---> As today's the world is growing faster and so the technologies, so doing anything manual is not preferable nowadays because manual doing is slower,less efficient and even          more time consuming.

---> Automation is the need of today's generation and here I came up with the automation within integration and deployment of our projects on the server-side so that whenever          Developer finishes writting the code or change something into the code, within one click, the changes will be updated on the server and client can see the changes on their        end without any breakdown in the site or anything else like that. 

# Requirements
# Tools & Technologies Used
  Continuous Integration Tools used to accomplish this automation are as follows:-
  1. GIT
  2. GITHUB
  3. JENKINS
  
  * GIT -  <a href="https://en.wikipedia.org/wiki/Git">GIT</a> is an open-source tool developers install locally to manage source code. 
  * GITHUB - <a href="https://en.wikipedia.org/wiki/GitHub">Github</a> is an online service to which developers who use Git can connect and upload or download resources. 
  * JENKINS - <a href="https://en.wikipedia.org/wiki/Jenkins_(software)">Jenkins</a> is used to build and test your software projects continuously making it easier for developers               to integrate changes to the project, and making it easier for users to obtain a fresh build.
  
  Technology which I used here for continuous deployment is  <b>DOCKER Containerization</b> and OS I used here is  <b>RHEL8</b> 
  
  ![](New%20folder/git_github_jenkins_docker_img.png)
      
  
# Pre-Requisites for this Project 
  Although this project is very easy to build but all you need is a basic understanding of the concepts of git,github,jenkins,docker and rhel8 and also how to configure and setup   all these in your system. If you know that, then follow the methodology given below to make it happen on your own.  
  

# Working  
We have to create 3 Jobs here on Jenkins:-
<br><b>JOB 1</b>
<br>If Developer push to dev branch then Jenkins will fetch from dev and deploy on dev-docker environment.

 <b>JOB 2</b>
<br>If Developer push to master branch then Jenkins will fetch from master and deploy on master-docker environment.
<b>Note</b>- Both dev-docker and master-docker environment are on different docker containers.

 <b>JOB 3</b>
<br>Manually the QA team will check (test) for the website running in dev-docker environment. If it is running fine then Jenkins will merge the dev branch to master branch and trigger <b>job 2</b>



  
  
