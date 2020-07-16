# Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER

## ABOUT
In today's fast-paced world, automation provides us with the speed and accuracy we need. The greater all industries access to Automation, the greater our lives become on the whole.

This project is about creating an automatic setup for an organization.

In this project, three aspects are considered which includes

how a developing team works on a central version controlling system
how a webpage is tested by the Quality Assurance Team, and then
how a webpage is deployed finally for the clients.


## OBJECTIVE
Create a setup in which once the developer will commit the code, it will be pushed automatically to GitHub.

And then Jenkins will pull the codes. Code of MASTER BRANCH will be deployed in the webserver and the code of the DEVELOPER BRANCH will be displayed to the Quality and Assurance Team.

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/flowchart%20(1).jpg)
Once QA Team will approve the design in Developer Branch, it will be merged to Master Branch automatically.



## WORK PROCESS


TOOLS USED
For Automation: JENKINS
For Containerization: DOCKER
For Repository Hosting: GitHub
For Version controlling: Git


________________________

AUTOMATIC PUSH IN GIT
Here, we can see initially both the branches are at the same commit level.

No alt text provided for this image
No alt text provided for this image
Then the developer will clone the repository in his system using the following command.

No alt text provided for this image
In the following way, a post-commit file will be created which will automatically push the repository once a developer commits.

No alt text provided for this image
The following are the changes made by the developer.

No alt text provided for this image
RESULT OF POST COMMIT

No alt text provided for this image
In the above picture, as soon as the developer enters the command to commit the changes, it is also pushed and the changes are reflected in GitHub.


JENKINS JOB DESCRIPTION
No alt text provided for this image
Points To Remember:

You have already downloaded the GIT plugin in Jenkins.
Make sure to run following command in RedHat Base OS to start Docker services.
No alt text provided for this image
__________________

There are three independent jobs (no job chaining).

No alt text provided for this image
__________________

The jobs are explained in detail as follows:

**JOB1**

This job will pull the code files from the MASTER BRANCH and then will launch a container using the httpd docker image for final production.

No alt text provided for this image
Link Jenkins with MASTER BRANCH to pull final files.

No alt text provided for this image
Poll SCM will keep checking every minute for any updates.

Remote Build is used, as JOB3 has to trigger JOB1.

No alt text provided for this image
Bash commands to launch a container for deploying webpage on httpd server for clients.

RESULT OF JOB 1

No alt text provided for this image
As we can see, this build successfully launched the "final_display" container which launches the webpage at port number 8084.

The webpage is showing initial commits.



**JOB2**

This job will pull the code files from the DEV BRANCH. Then docker will launch a container using the httpd docker image to a specific port number for the Quality Assurance Team to test the webpage.

No alt text provided for this image
Pulling files from DEVELOPER BRANCH.

No alt text provided for this image
Poll SCM will keep checking every minute for any updates.

We can also use GitHub hooks to inform Jenkins about any modifications.

No alt text provided for this image
Bash commands to launch a container for deploying webpage for QA Team on a different port.

RESULT OF JOB 2

No alt text provided for this image
This build successfully launched a "test_env" container which launches the webpage at port number 8085.

Also, there is no change in the previously launched final webpage at port number 8084 (top-right window).



**JOB3**

Once the Quality Assurance Team approves the web page, they will start the job. And this job will then merge the DEVELOPER BRANCH to MASTER BRANCH and will trigger Job1 which will deploy the updated final webpage in httpd webserver. 

No alt text provided for this image
Link to DEV branch in GitHub.

No alt text provided for this image
Specify the "Pre-build actions", for merging the branches in GitHub as shown in the above image.

No alt text provided for this image
There is no need for any build trigger as this job will be built manually by the QA Team.

No alt text provided for this image
Bash commands to trigger JOB1 and delete already deployed final webpage.

No alt text provided for this image
RESULT OF JOB 3

No alt text provided for this image
Here we can see, as soon as Job3 is completed, it has triggered Job1 (right window)

No alt text provided for this image
Also, both the windows of final production (port_no 8084) and test environment (port_no 8085) have the same content, i.e. branches have been merged.



<>FUTURE SCOPE
In this project, I have considered only the following things for automation:

pushing repository after committing.
launching new file for testing
launching final file for clients
There are many other stages, many testing levels in the lifecycle of a software project.

There is a wide scope to make the entire process automatic.
