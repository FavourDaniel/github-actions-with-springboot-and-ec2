# Github-Actions-with-Springboot-and-EC2
![Frame 1 (5)](https://user-images.githubusercontent.com/89241109/180608741-a66186cc-a5ee-479a-987f-6bede1720e45.png)

This project demonstrates how to create a continuous integration pipeline such that if a change is made to the repository, updates are automatically built and pushed to the ec2 instance.

---
## Pre-requisites & Installation guide
Working knowledge of CICD, aws, a code editor.

### Create an EC2 instance
- In your security group inboud rules setting, open ssh for port 22 - custom and open tcp for port 80 - anywhere
- Allocate an elastic IP address to your instance to provide you with a static ip (optional)
### 

---
# Project Setup
### Step 1: Clone this repository
```
git clone <REPO_URL>
```
### Step 2: Edit the repo by adding your instance details where expected.

### Step 3: ssh into your ec2 instance
```
sudo ssh -i "yourkeypairname.pem" instancetype@instancepubliciddress.region.compute.amazonaws.com
```
If you do not understand the above, the below is an example
```
sudo ssh -i "cicdkey.pem" ubuntu@ec3-4-5-22-13.us-east-1.compute.amazonaws.com
```
NB: ensure you are in the directory where your key pair is present.

### Step 4: Setup Github Actions
Push the project to github and in the settings tab, select Actions >> Runners >> Then create a new self-hosted runner

![cicd 1](https://user-images.githubusercontent.com/89241109/181905295-dba86632-5248-4653-8acb-84575e4e90a4.png)

After creating the self-hosted runner, select the runner image depending on what kind of instance you created, the copy and paste all the commands under ```Download``` to your ec2 instance which you have sshed into
![cicd2 1](https://user-images.githubusercontent.com/89241109/181905305-29f3417f-dbf3-4234-bcb4-0c8bc09a6a59.png)

Once you have copied and pasted the ```Download``` commands, copy and past the ```Configure``` commands as well
![cicd3 1](https://user-images.githubusercontent.com/89241109/181905312-79268e5f-5e41-4cce-853a-834eeae79e0f.png)

### Step 5: Further Installations
After setup, some specifics in the project need to be installed for the runner to do its work. If you ```ls``` you would see the files that the runner presently contains.
```
sudo ./svc.sh install
```
After installing in, start it
```
sudo ./svc.sh start
```
This command automatically connects your project with Github/the repo.

### Step 5: Setup Workflow
The workflow for this project has already been setup but if you would like to set it up your own, delete the ```maven.yml``` file.
Navigate to actions tab on the in the repository and select ```Java with Maven```. 
![cicd4 1](https://user-images.githubusercontent.com/89241109/181905910-80c574ac-8b83-4eaa-979e-ee3448403cc3.png)

Inside the workflow, in jobs >> builds >> runs-on, change ```ubuntu-latest``` to ```self-hosted``` because we are using a self-hosted runner. You can take out the ```pull_request: branches``` since it is not necessary, then commit.
![cicd5 1](https://user-images.githubusercontent.com/89241109/181905914-52a72a71-599d-422f-aa57-f6094d457831.png)

### Step 6: Installing dependencies
Jdk needs to be installed in the instance. In the actions-runner directory, ```cd`` and update pacakages first
```
sudo apt update
```
Then
```
sudo apt install maven openjdk-11-jre openjdk-11-jdk
```
With dependencies in place, builds made will run and be visble on github

You can check your instance ip address to view the site.
