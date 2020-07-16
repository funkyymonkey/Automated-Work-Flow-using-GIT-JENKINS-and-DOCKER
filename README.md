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


#### TOOLS USED
For Automation: **JENKINS**
For Containerization: **DOCKER**
For Repository Hosting: **GitHub**
For Version controlling: **Git**


________________________

#### AUTOMATIC PUSH IN GIT
Here, we can see initially both the branches are at the same commit level.

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/initial%20(1).PNG)
![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/initial%20(2).PNG)

Then the developer will clone the repository in his system using the following command.

![IMAGE]()
In the following way, a post-commit file will be created which will automatically push the repository once a developer commits.

![IMAGE]()
The following are the changes made by the developer.

![IMAGE]()
RESULT OF POST COMMIT

![IMAGE]()
In the above picture, as soon as the developer enters the command to commit the changes, it is also pushed and the changes are reflected in GitHub.


#### JENKINS JOB DESCRIPTION
![IMAGE]()
Points To Remember:

You have already downloaded the GIT plugin in Jenkins.
Make sure to run following command in RedHat Base OS to start Docker services.
![IMAGE]()
__________________

There are three independent jobs (no job chaining).

![IMAGE]()
__________________

The jobs are explained in detail as follows:

_**JOB1**_

This job will pull the code files from the MASTER BRANCH and then will launch a container using the httpd docker image for final production.

![IMAGE]()
Link Jenkins with MASTER BRANCH to pull final files.

No alt text provided for this image
Poll SCM will keep checking every minute for any updates.

Remote Build is used, as JOB3 has to trigger JOB1.

No alt text provided for this image
Bash commands to launch a container for deploying webpage on httpd server for clients.

_**RESULT OF JOB 1**_

![IMAGE]()
As we can see, this build successfully launched the "final_display" container which launches the webpage at port number 8084.

The webpage is showing initial commits.



_**JOB2**_

This job will pull the code files from the DEV BRANCH. Then docker will launch a container using the httpd docker image to a specific port number for the Quality Assurance Team to test the webpage.

![IMAGE]()
Pulling files from DEVELOPER BRANCH.

![IMAGE]()
Poll SCM will keep checking every minute for any updates.

We can also use GitHub hooks to inform Jenkins about any modifications.

![IMAGE]()
Bash commands to launch a container for deploying webpage for QA Team on a different port.

_**RESULT OF JOB 2**_

![IMAGE]()
This build successfully launched a "test_env" container which launches the webpage at port number 8085.

Also, there is no change in the previously launched final webpage at port number 8084 (top-right window).



_**JOB3**_

Once the Quality Assurance Team approves the web page, they will start the job. And this job will then merge the DEVELOPER BRANCH to MASTER BRANCH and will trigger Job1 which will deploy the updated final webpage in httpd webserver. 

![IMAGE]()
Link to DEV branch in GitHub.

![IMAGE]()
Specify the "Pre-build actions", for merging the branches in GitHub as shown in the above image.

![IMAGE]()
There is no need for any build trigger as this job will be built manually by the QA Team.

![IMAGE]()
Bash commands to trigger JOB1 and delete already deployed final webpage.

![IMAGE]()

_**RESULT OF JOB 3**_

![IMAGE]()
Here we can see, as soon as Job3 is completed, it has triggered Job1 (right window)

![IMAGE]()
Also, both the windows of final production (port_no 8084) and test environment (port_no 8085) have the same content, i.e. branches have been merged.



## FUTURE SCOPE
In this project, I have considered only the following things for automation:

pushing repository after committing.
launching new file for testing
launching final file for clients
There are many other stages, many testing levels in the lifecycle of a software project.

There is a wide scope to make the entire process automatic.
