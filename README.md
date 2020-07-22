# Problem Statement
---> As today's the world is growing faster and so the technologies, so doing anything manual is not preferable nowadays because manual doing is slower,less efficient and even        more time consuming.

---> Automation is the need of today's generation and here I came up with the automation within integration and deployment of our projects on the server-side so that whenever        Developer finishes writting the code or change something into the code, within one click, the changes will be updated on the server and client can see the changes on their      end without any breakdown in the site or anything else like that. 


# Tools & Technologies Used
  Continuous Integration Tools used to accomplish this automation are as follows:-
<br>1. GIT - <a href="https://en.wikipedia.org/wiki/Git">GIT</a> is an open-source tool developers install locally to manage source code. 
<br>2. GITHUB - <a href="https://en.wikipedia.org/wiki/GitHub">Github</a> is an online service to which developers who use Git can connect and upload or download resources. 
<br>3. JENKINS - <a href="https://en.wikipedia.org/wiki/Jenkins_(software)">Jenkins</a> is used to build and test your software projects continuously making it easier for developers to integrate changes to the project, and making it easier for users to obtain a fresh build.
<br>4. DOCKER CONTAINERIZATION - Containerization is a technology which I used here for Continuous Deployment. 
<br>5. RHEL8 - OS used 
  
  ![](New%20folder/git_github_jenkins_docker_img.png)
      
  
# Pre-Requisites for this Project 
  Although this project is very easy to build but all you need is a basic understanding of the concepts of git,github,jenkins,docker and rhel8 and also how to configure and       setup   all these in your system. If you know that, then follow the methodology given below to make it happen on your own.  
  

# Methodology 
  We have to create 3 Jobs here on Jenkins:-
  <br><b>JOB 1</b>
  <br>If Developer push to dev branch then Jenkins will fetch from dev and deploy on dev-docker environment.
  <br><b>JOB 2</b>
  <br>If Developer push to master branch then Jenkins will fetch from master and deploy on master-docker environment.
  <br><b>Note</b>- Both dev-docker and master-docker environment are on different docker containers.
  <br><b>JOB 3</b>
  <br>Manually the QA team will check (test) for the website running in dev-docker environment. If it is running fine then Jenkins will merge the dev branch to master branch and    trigger <b>JOB 2</b>


# Step-by-Step Working Procedure
  ![](New%20folder/1.png)
  First of all, Create a Job in Jenkins which will create 2 directories in Rhel8, one for storing the data of Sub-Developer i.e. Developer Branch and another for storing the       data of Main Developer i.e. Master Branch.
  
  ![](New%20folder/2.png)
  Here you can see that Developer finishes writting the code for their website and when he commit the code in GIT, automatically the code will push to the GITHUB through post-     commit actions and also it will triggers the Job1 i.e. Developer Job in Jenkins.
  
  <h1 style="background-color:Gray;"><br>In the Developer Job i.e. Job1, you have to write the following code in the execute shell-
  <br>sudo cp -vrf * /developer
  <br>if sudo docker ps | grep webdev
  <br>then 
  <br>    echo "Already Running"
  <br>else
  <br>    sudo docker run -dit -p 8081:80 -v /developer:/usr/local/apache2/htdocs/ --name webdev httpd
  <br>fi 
  </p></h1>
  
  <br>Above code of the execute shell will first copy all the data that jenkins downloaded from GITHUB repo. of Sub-Developer to the directory of Developer that we created          earlier in Rhel8. After copying data, it will launch a container through docker using httpd image so to deploy Developer's website on Dev-Docker environment. 
  
  



  
  
