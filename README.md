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

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/git%20(1).PNG)
In the following way, a post-commit file will be created which will automatically push the repository once a developer commits.

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/git%20(2).PNG)
The following are the changes made by the developer.

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/git%20(3).PNG)
RESULT OF POST COMMIT

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/git%20output.PNG)
In the above picture, as soon as the developer enters the command to commit the changes, it is also pushed and the changes are reflected in GitHub.


#### JENKINS JOB DESCRIPTION
![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/flowchart%20(2).jpg)
Points To Remember:

You have already downloaded the GIT plugin in Jenkins.
Make sure to run following command in RedHat Base OS to start Docker services.
![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/extra%20(2).PNG)
__________________

There are three independent jobs (no job chaining).

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/extra%20(1).PNG)
__________________

The jobs are explained in detail as follows:

_**JOB1**_

This job will pull the code files from the MASTER BRANCH and then will launch a container using the httpd docker image for final production.

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job1%20(1).PNG)
_Link Jenkins with MASTER BRANCH to pull final files._

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job1%20(2).PNG)
_Poll SCM will keep checking every minute for any updates._

_Remote Build is used, as JOB3 has to trigger JOB1._

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job1%20(3).PNG)
_Bash commands to launch a container for deploying webpage on httpd server for clients._

_**RESULT OF JOB 1**_

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job1%20output.PNG)
_As we can see, this build successfully launched the "final_display" container which launches the webpage at port number 8084._

_The webpage is showing initial commits._



_**JOB2**_

This job will pull the code files from the DEV BRANCH. Then docker will launch a container using the httpd docker image to a specific port number for the Quality Assurance Team to test the webpage.

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job2%20(1).PNG)
_Pulling files from DEVELOPER BRANCH._

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job2%20(2).PNG)
_Poll SCM will keep checking every minute for any updates._

_We can also use GitHub hooks to inform Jenkins about any modifications._

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job2%20(3).PNG)
_Bash commands to launch a container for deploying webpage for QA Team on a different port._

_**RESULT OF JOB 2**_

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job2%20output.PNG)
_This build successfully launched a "test_env" container which launches the webpage at port number 8085._

_Also, there is no change in the previously launched final webpage at port number 8084 (top-right window)._



_**JOB3**_

Once the Quality Assurance Team approves the web page, they will start the job. And this job will then merge the DEVELOPER BRANCH to MASTER BRANCH and will trigger Job1 which will deploy the updated final webpage in httpd webserver.

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job3%20(1).PNG)
_Link to DEV branch in GitHub._

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job3%20(2).PNG)
_Specify the "Pre-build actions", for merging the branches in GitHub as shown in the above image._

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job3%20(3).PNG)
_There is no need for any build trigger as this job will be built manually by the QA Team._

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job3%20(4).PNG)
_Bash commands to trigger JOB1 and delete already deployed final webpage._

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job3%20(5).PNG)

_**RESULT OF JOB 3**_

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job3%20output%20(1).PNG)
_Here we can see, as soon as Job3 is completed, it has triggered Job1 (right window)_

![IMAGE](https://github.com/funkyymonkey/Automated-Work-Flow-using-GIT-JENKINS-and-DOCKER/blob/master/task%20snaps/job3%20output%20(2).PNG)
_Also, both the windows of final production (port_no 8084) and test environment (port_no 8085) have the same content, i.e. branches have been merged._

# _THANK YOU!!_
