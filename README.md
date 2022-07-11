# Continuous improvement from Dev to Production

 <img src="images/CIdemo.jpg" width="750" height="450" />


<br>
This is a tutorial to setup a sandbox environment that focusses on <br>
how "Dynatrace Automated SLO Evaluation" can be implemented into an <br>
Automated Software Delivery Process. <br> 
<br>
<br>
The functions outside the SLO Evaluation like Deployments and <br>
Testing are not necessarily best practise, they were designed to serve the Purpose <br>
to Quickly Test or Demo the Slo Evaluation Process from Dev to Production without <br>
having to wait hours for a delivery step like Testing to complete. <br>
<br>


# Prerequisites  
<br>
 
### The following Accounts and Tokens are needed to create this Sandbox 
<br>

|  Vendor      | Prerequisite |
| ----------- | ----------- |
| Dynatrace   | Account, Api Token, Data Ingest Token        |
| Dynatrace Cloudautomation  | Account, Api Token      |
| AWS  | Account      |
| Dockerhub  | Account, Access Token      |
| Github  | Account, Personal Access Token      |

<br>
Note! You can save some time if you collect all the needed URLs and Api-Tokens Pre Sandbox Installation.<br>
Store them safely with keepaas https://keepass.info/

<br>

# Videos
There is a fast paced video available that goes through the sandbox setup below under the following link: <br>
[Sandbox Install Video](https://dynatrace-my.sharepoint.com/:v:/p/daniel_braaf/ES5iB75D4UdIhawT1EYO6tABrj_Mgo43f_-fhPNS-W9b7Q?e=DlbEQA) <br>

The Sandbox Demo in action: <br>
[Sandbox Demo](https://dynatrace-my.sharepoint.com/:v:/p/daniel_braaf/ESq6-0d4v0ZFjnshNOL6qukBenmVuWrxhu_ZNYH4Nv6daA?e=gW2dsL) <br>

# Sandbox Setup
<br>
The Sandbox Setup takes about 15 - 20min <br>
Most of the installation is Automated, there are just a few manual steps to take <br>
like settings variables and secrets. <br> <br>

## Create a Repository in Docker Hub
<br>

* Log in to hub.docker.com.
* Click Create a Repository on the Docker Hub welcome page.
* Name it <your-username>/my-private-repo. (any name of your choice)
* Set the visibility to Public.

  <img src="images/index-create-repo.png" width="300" height="230" />
<br>

## Create a Github Repository from Template

<br>

* Login to your GitHub account.
* Navigate to the https://github.com/danatrace/continuousimprovement repository.
* Click the "use this Template Button", give it any name that you would like.
* Now, navigate to your new repository. 

<br>

## Enable Issues for your Github Repository

* Navigate to the main page of the repository. Under your repository name click Settings,
  Under Features, select the Issues checkbox.

  <img src="images/png;base64b2b0394caca4693b.png" width="600" height="200" />

<br>

## Enable Github Workflow Actions for your Github Repository

* Navigate to the home of your new Github Repository and click on Actions
* Click the Green button to enable Github Workflows



  <img src="images/pasted image 0 (1).png" width="380" height="240" />

<br>


## Create Github Environment Variable Secrets



* Navigate to the home of your Github Repository and click on Settings
* Click Secret -> Actions in the menu on the left

  <img src="images/pasted image 0 (4).png" width="380" height="300" />

<br>

* Click on the “New repository secret” button and create the following secrets

    |  Variable    | info | where to find it |
    | ----------- | ----------- | ----------- |
    | CA_TOKEN   |  Cloudautomation Token   | Cloudautomation UI
    | DOCKERHUB  |  Dockerhub Token   | Dockerhub
    | DOCKER_USER   | Dockerhub User     | Dockerhub
    | DT_API_TOKEN  | Dynatrace Api Token   | Access Token in Dynatrace
    | DT_URL   | Dynatrace URL  | for example https://xxxxx.live.dynatrace.com
    | DT_API_URL  | Dynatrace API URL    | for example https://xxxxx.live.dynatrace.com/api
    | DT_CA_URL   | Cloudautomation URL    | for example https://xxxx.cloudautomation.live.dynatrace.com
    | DT_DATAINGESTTOKEN  | Dynatrace Data Ingest Token base64 encoded   | In Dynatrace click on create a new Active Gate, in the setup page create new tokens and download the dynacube.yaml In the Dynacube.yaml you will fin d the base64 encoded Data ingest token
    | DT_API_TOKEN_B64   |  Dynatrace Api Token   | In Dynatrace click on create a new Active Gate, in the setup page create new tokens and download the dynacube.yaml In the Dynacube.yaml you will fin d the base64 encoded Data ingest token
    | WORKFLOW_TOKEN  | Github Personal Access Token    | Githui UI


<br>

## Create Github Project (by running workflow)

* Navigate to the home of your Github Repository and click on Actions
* In the Workflow Overview click on the "Create Project Board" Workflow in the Menu

  <img src="images/pasted image 0 (6).png" width="200" height="200" />

<br>

* Click the Run Workflow Button on the right, chose the Master Branch and Click  the Green Run  Workflow Button

  <img src="images/pasted image 0 (7).png" width="200" height="150" />

<br>

* Wait until the Workflow run has finished

  <img src="images/pasted image 0 (8).png" width="300" height="120" />

<br>

* Click on Projects in the Menu
* Click on Projects (Classic)
* Click on the Simplenodeservice Project

  <img src="images/pasted image 0 (11).png" width="400" height="100" />

<br>


* Put the Project Columns into the right order via drag and drop (When the workflow creates the project it doesn’t keep the order) todo, in progress, Ready for Review, Done, Shipped


  <img src="images/pasted image 0 (12).png" width="600" height="100" />

<br>


## Create Github Environment


* Navigate to the home of your Github Repository and click on Settings
* Click Environments in the left Menu

  <img src="images/pasted image 0 (14).png" width="300" height="200" />
<br>

* Click on the “New Environment” Button

  <img src="images/pasted image 0 (15).png" width="350" height="120" />
<br>

* Create Environment with the Name “production-approval”

  <img src="images/pasted image 0 (16).png" width="300" height="140" />
<br>

* Activate Required reviewers and add yourself 

  <img src="images/pasted image 0 (17).png" width="550" height="300" />
<br>

## Create new Github Runner

* Navigate to the home of your Github Repository and click on Settings
* On the settings page click on Actions - Runners

  <img src="images/pasted image 0 (19).png" width="300" height="300" />
<br>

* In the runners overview click on the green “New Self-hosted runner” button

  <img src="images/pasted image 0 (20).png" width="500" height="100" />
<br>

* On the Create Runners page select “Linux”

  <img src="images/pasted image 0 (21).png" width="500" height="200" />
<br>


* Copy the token from the Configure script

  <img src="images/copytoken2.png" width="500" height="150" />
<br>



* Copy the entire Content of the “aws/userdatafile.sh” file in your Github Repository to a local text file editor,  replace "< token >" with the token you have copied from the configure script and "< github repourl >" with the url to the repository you have created. Save the script we wil need it for installation of the AWS instance.

  <img src="images/userdaafiesh.png" width="650" height="200" />
<br>

* Do not close the Github Runner Installation page until the installation of the AWS Instance in the next step has been created.

<br>
<br>

## AWS Set Up

* Logon to the AWS Management Console and Navigate to EC2
* Click on the “Launch Instances” button

  <img src="images/pasted image 0 (22).png" width="500" height="100" />
<br>

* Chose AMI (Amazon Linux 2 AMI Kernel 4)

  <img src="images/pasted image 0 (23).png" width="500" height="110" />
<br>

* Choose Instance Type T3.xlarge and click next


  <img src="images/pasted image 0 (24).png" width="500" height="110" />
<br>


* Scroll to the Bottom of the page until you get to Advanced Details - User data, paste the content
  of the userdatafiel.sh with the replaced token and github url into the user data field.

  <img src="images/pasted image 0 (24).png" width="500" height="110" />
<br>


* Add Storage (50GB General Purpose SSD) and click on next
* Optional Add Tags
* Create a Security Group with the following entries (click my IP will enter your IP address making the instance only available from your ip address!) Review and Launch instance.

  <img src="images/pasted image 0 (26).png" width="500" height="110" />
<br>

* Wait until your instance has passed the Initializing State and checks have passed.
* Go back to your Github runner install page and click on Actions - Runners.  The Runner started and should be in Idle state as seen below (with a different ip address than in the picture)

  <img src="images/pasted image 0 (28).png" width="500" height="150" />
<br>


## Start Github Install Workflow 


The Workflow will create the following Demo Content:

* Dashboards (Dynatrace)
* Auto-Tags (Dynatrace)
* Management Zones (Dynatrace)
* Alerting Profiles (Dynatrace)
* Anomally detection metrics (Dynatrace)
* Custom Metrics (Dynatrace)
* A single node K3S Kubernetes Cluster (AWS instance)
* A Dynatrace Agent (AWS instance)
* A Dynatrace Active Gate (AWS instance)
* A Cloud Automation Project (Dynatrace)
* SLOs in Cloud Automation (Dynatrace)
* A Service in Cloud Automation (Dynatrace)

<br>

* Navigate to the home of your Github Repository and click on Actions
* In the Actions view Click on the “Install Demo” Workflow

   <img src="images/pasted image 0 (30).png" width="200" height="200" />
<br>

* Now click the”Run workflow” button
* Chose run from “Master” Branche
* Click on the Green Run Workflow button

   <img src="images/pasted image 0 (31).png" width="200" height="130" />
<br>

* Wait until workflow finished

   <img src="images/pasted image 0 (32).png" width="500" height="150" />
<br>

## Create Webhooks in Cloudautomation

* Go to your Cloudautomation instance
* the Install Workflow has created a project called "slo-evaluation" and "deployment-gates" go into the slo-evaluation project and click on settings, in settings click on secrets and create a secret called Dynatraceapitoken (a second one to the already existing one, as this one is for the webhook only) with the key DT_API_TOKEN and
the scope keptn-webhook-service
* Go back to settings, in settings click on integrations and chose Webhook-Service

   <img src="images/webhookservice.png" width="500" height="150" />
<br>


* scroll to the bottom of the page and click on "add subscription"
* in Add Subcription select Task evaluation and Task suffix finished
* Filter by stages dev, staging, production
* Requst Method POST
* enter the Url  < your dnyatrace url >/api/v1/entity/infrastructure/custom/custom:releaseevaluationscore
* add headers accept = application/json, Authorization=Api-Token < your dynatrace api token secret > (Chose the key symbol and use the key created ealier), content-type=application/json
* add Custom Payload
```
{
    "type": "test",
    "series": [
        {
            "timeseriesId": "custom:releaseevaluationscore",
            "dimensions": {
                "Score": {
                    {.data.evaluation.score
                    }
                },
                "Result": "{{.data.result}}",
                "Passed": 0,
                "Releaseversion": "{{.data.labels.buildId}}",
                "Buildversion": "{{.data.labels.buildId}}",
                "Buildnumber": {
                    {.data.labels.buildId
                    }
                },
                "Evaluationtime": "{{.time}}",
                "Application": "simplenodeservice-{{.data.stage}}"
            },
            "dataPoints": [
                [
                    {
                        {.data.labels.evaltime
                        }
                    },
                    {
                        {.data.evaluation.score
                        }
                    }
                ]
            ]
        }
    ]
}
```
* Remove all line breaks from the json file so its a one liner (You can use the one liner below)
 ```
 {  "type": "test",  "series": [    {      "timeseriesId": "custom:releaseevaluationscore",      "dimensions": {        "Score" : {{.data.evaluation.score}},        "Result" : "{{.data.result}}",        "Passed" : 0,        "Releaseversion": "{{.data.labels.buildId}}",        "Buildversion": "{{.data.labels.buildId}}",        "Buildnumber":  {{.data.labels.buildId}},        "Evaluationtime": "{{.time}}",        "Application" : "simplenodeservice-{{.data.stage}}"              },      "dataPoints" : [[ {{.data.labels.evaltime}}, {{.data.evaluation.score}} ]]                  }  ]}   
 ```
 
 

* Scroll to the bottom of the page and click the "update subcription" button
* Repeat the same steps as above for the deployment-gates project but with the following content as
payload:

```
{
    "type": "test",
    "series": [
        {
            "timeseriesId": "custom:releaseevaluationscore",
            "dimensions": {
                "Score": {
                    {.data.evaluation.score
                    }
                },
                "Result": "{{.data.result}}",
                "Passed": 0,
                "Releaseversion": "{{.data.labels.buildId}}",
                "Buildversion": "{{.data.labels.buildId}}",
                "Buildnumber": {
                    {.data.labels.buildId
                    }
                },
                "Evaluationtime": "{{.time}}",
                "Application": "simplenodeservice-{{.data.stage}}-DG"
            },
            "dataPoints": [
                [
                    {
                        {.data.labels.evaltime
                        }
                    },
                    {
                        {.data.evaluation.score
                        }
                    }
                ]
            ]
        }
    ]
}

```
Here the one liner for the second wehbook
 ```
 {  "type": "test",  "series": [    {      "timeseriesId": "custom:releaseevaluationscore",      "dimensions": {        "Score" : {{.data.evaluation.score}},        "Result" : "{{.data.result}}",        "Passed" : 0,        "Releaseversion": "{{.data.labels.buildId}}",        "Buildversion": "{{.data.labels.buildId}}",        "Buildnumber":  {{.data.labels.buildId}},        "Evaluationtime": "{{.time}}",        "Application" : "simplenodeservice-{{.data.stage}}-DG"              },      "dataPoints" : [[ {{.data.labels.evaltime}}, {{.data.evaluation.score}} ]]                  }  ]}   
 ```

## Create Github Branches for Staging and Dev
 
* Navigate to the main page of your repository 
* Create a "dev" and "staging" branche from the master Branche, to do so click on the Master Branche Button on the main page
  of your repository, then click view all branches, click on the New Branche button. 
 
 
## Set Workflow Variables

* Navigate to the home of your Github Repository
* Change Current Branche to “dev”

   <img src="images/pasted image 0 (33).png" width="150" height="50" />
<br>



* Switch into directory .”github/workflow”

   <img src="images/pasted image 0 (34).png" width="300" height="250" />
<br>


* Open the dev.yml file for edit

   <img src="images/pasted image 0 (35).png" width="300" height="250" />
<br>


* Set the env: variables

|  Variable    | info | 
| ----------- | ----------- | 
| GITHUB_PROJECT_URL | https url to the Project of your Github Repo created earlier 
| DOCKER_REPO_URL | Link to the Docker Hub Repo created in the first step 
| DT_URL | Dynatrace URL | 
| DOCKER_TAG | Docker tag of your Docker hub repo created in the first step 


* Commit the change with the following commit message “demo first” This will start the Demo Workflow and Deploy the Initial Application to Dev, Staging <br> <br>
   <img src="images/demofirst.png" width="250" height="250" />
<br>

## Follow Initial Demo Workflow Run
Commiting the changes with the commit message "demo first" will start Initial Demo run. <br>
The first time you kick off the demo there are some initialization steps done and the runs take <br>
significantly longer than when running the demo scenarios later on. <br>

The Initial Demo run will 
* Run the Deployment to dev, have a successful slo evaluation and then merges the dev with the staging branche which kick off
* The Staging Deployment that will also have a successful slo evaluation run and wait for your approval, after you approve
* the Production Workflow will run

You can use the initial demo run to check if everything works. <br>
How this is done can be seen in the following video: [Inital Demo Run](https://dynatrace-my.sharepoint.com/:v:/p/daniel_braaf/ESkzogAqeNREg_1vNaIZhkABf5gTg5qEQsgAClgTuFm3QQ?e=twQBtt) <br>
<br>

## Demo Functions
The Sandbox Demo has some builtin functions to play through different scenearios. The Functions are controlled by the commit message. <br>
Note! A demo in this Sandbox is always started by making a change to the dev branch, this activates the deployment workflows <br>
in a true gitops fashion
<br>
<br>


|  Commitmsg   | Functionality | 
| ----------- | ----------- | 
| demo first | Used for the very first run after installation, used to initialize the demo and test if everything works. The Workflows take significantly longer during the initial run and should not be seen as a demo but part of the installation. This only needs to be done the very first time the demo is run after the installation 
| demo | All SLO evaluations in all stages will succeed! The Demo Deploys the new code to Dev, then runs an slo evaluation, the evaluation succeeds and merges the dev branche into the staging branche, which activates the staging deployment workflow, here we deploy to staging, run another evaluation, the evaluation succceeds and the workflow waits for approval. Approval of the workflow will merge the staging branche into the production branche and start deployment to production where first we check if Production is ready to be deployed to by running a pre deployment evaluation, the evaluation succeeds and the deployment to production succeeds. after the deployment to production we run another last slo evaluation to make sure our new changes run smoothly in production.
| demo faildev | the slo evaluation in dev will fail with High CPU and Memory usage, this will crate an issue with a link to the root cause of the problem, we click the link, identify and fix the problem. This is meant to show the advantages Dynatrace SLO evaluation has for Dev, Automatically Identify issues based on slos and provide a fast response with the root cause so the problem can be identified and fixed fast!  | 
| demo failstaging | the slo evaluation in dev will be successful but fail in staging, due to the slo failing the new change is rolled back and an issue created with a link to the root cause of the problem in dynatrace. However since the problem is found in staging we have more people on board that will be notified about the issue. We most likely will have Dev, QA and the Release Manager made aware of the Problem.


