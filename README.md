# Github-actions-with-springboot-and-ec2
![Frame 1 (5)](https://user-images.githubusercontent.com/89241109/180608741-a66186cc-a5ee-479a-987f-6bede1720e45.png)

This project demonstrates how to create a continuous integration pipeline such that if a change is made to the repository, updates are automatically built and pushed to the ec2 instance.

---
## Pre-requisites & Installation guide
### Install git
https://git-scm.com/downloads

### Create an EC2 instance

### 

---
## Project Setup
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

Step 4: Setup Github Actions
Push the project t github and in the settings tab, select Actions >> Runners >> Then create a new self-hosted runner
