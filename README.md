<h1 align="center">Automated ELB creation from Jenkins<h1> 


# Deployment 3
September 16, 2023

By: Andrew Mullen

## Purpose:

Demonstrate the ability to run a Jenkins build and manually deploy to Elastic Beanstalk

## Steps:

### 1. Create your own Jenkins Server and install the following on the server:
   - Install "python3.10-venv"
   - Install "python-pip"
   - Install "unzip"

### 2. Create a multibranch pipeline and run the build for the application

- Jenkins is the main tool used in this deployment for pulling the program from the GitHub repository. Then building and testing the files to be deployed to Elastic Beanstalk.
- Creating a multibranch pipeline gives the ability to implement different Jenkinsfiles for different branches of the same project.
- A Jenkinsfile is used by Jenkins to list out the steps to be taken in the deployment pipeline.

- Steps in the Jenkinsfile are as follows:
  - Build
    - The environment is built to see if the application can run.
  - Test
    - Unit test is performed to test specific functions in the application


### 3. Follow the install AWS EB CLI instructions

- This is where run commands to automatically create the ELB instance that our application will run on
    - Using credentials
- The Build Stage built the environment for the application to run
    - See Troubleshooting for errors and resolution
- The Test Stage performed tests and found no errors
- The Packaging Stage, after receving confimation, zipped the files

### 4. Add 'Deploy' stage to the Jenkins file in Jenkins

- In Jenkins
    - Open the Jenkinsfile.
	- Add the following 
	 - `stage ('Deploy') { steps { sh '/var/lib/jenkins/.local/bin/eb deploy' } }`
	- Rerun the build

### 5. If redeployed successfully to Elastic Beanstalk, what changed?



## System Diagram:

To view the diagram of the system design/deployment pipeline, click [HERE](https://github.com/andmulLABS01/Deployment_3AM/blob/main/Depoyment3.drawio.png)

## Issues/Troubleshooting:

Demonstrate the ability to deploy to a fully automated Elastic Beanstalk instance

Resolution Steps:
- Check the Console Output in Jenkins
  - Click the Build, Console output
- Discovered the following:
  - Python3.10-venv not installed
  - ensurepip not available
- Installed Python3.10-venv on the terminal
  - `sudo apt install python3.10-venv`
- Rerun Jenkins build and was successful 


![alt text](https://github.com/andmulLABS01/Deployment_2AM/blob/main/dp2_error.PNG)


## Conclusion:

There are some optimizations that can be made to this depoyment.  One can be automating the creation of the Jenkins server, creating AWS IAM Roles, installing the AWS CLI,.
