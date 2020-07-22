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
  
  <br>In the Developer Job i.e. Job1, you have to write the following code in the execute shell-
  <br>sudo cp -vrf * /developer
  <br>if sudo docker ps | grep webdev
  <br>then 
  <br>    echo "Already Running"
  <br>else
  <br>    sudo docker run -dit -p 8081:80 -v /developer:/usr/local/apache2/htdocs/ --name webdev httpd
  <br>fi 
  
  <br>Above code of the execute shell will first copy all the data that jenkins downloaded from GITHUB repo. of Sub-Developer to the directory of Developer that we created          earlier in Rhel8. After copying data, it will launch a container(give any name say 'webdev') through docker using httpd image so to deploy Developer's website on Dev-Docker      environment. 
  
  Write the following code in the execute shell of Job2-
  <br>sudo cp -vrf * /master
  <br>if sudo docker ps | grep webmaster
  <br>then 
  <br>    echo "Already Running"
  <br>else
  <br>   sudo docker run -dit -p 8082:80 -v /master:/usr/local/apache2/htdocs/ --name webmaster httpd
  <br>fi    
  
  <br>This will launch the container for master branch and deploy the code of master on the master-docker environment. Here you can see the website of master.
  
  ![](New%20folder/3.png)
  
  Once the Quality Assurance Team give the verification check for the website running in Dev-Docker env and will approve the changes that are made to this website to be merged     with the master's website then you have to go for Job3. Job3 will merge both the branches(dev and master) and trigger the master's Job i.e. Job2 for the changes to be           reflected in the main website and so the client can see the updations made in the website.
  
  For merging, you have to follow this-
  
  
  ![](New%20folder/4.png)
  
  This will successfully merge both the branches and the client can now see the updated website. See here:-
  
  
  ![](New%20folder/5.png)
  
  <b>Note</b>- You can face issues while merging the branches in regard of merge conflicts. <br>But Don't worry I will explain you what is Merge Conflicts and how you can                      resolve them.
  
  Merge Conflicts is nothing but the conflicts arises when at the same time, same line of code is manipulated by multiple Developers within the same repository. At that time, It   becomes difficult for the GITHUB to decide which is the final change that GITHUB needs to keep. That's the reason it gives conflicts error messages. But you can resolve them     by simply commiting the final code that you need to be there in your website and remove everything that you don't want to be part of your website. After commiting, GITHUB will   get to know the finalise product(code) and then it will merge the branches for you easily. For more info about merge conflicts you can visit <a href="https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line">here</a>
 
  
  
  



  
  
