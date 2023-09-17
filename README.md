<h1 align="center">Automated ELB creation from Jenkins<h1> 


# Deployment 3
September 16, 2023

By: Andrew Mullen

## Purpose:

Demonstrate the ability to deploy to a fully automated Elastic Beanstalk instance

## Steps:

### 1. Create your own Jenkins Server and install the following on the server:
   - Install "python3.10-venv"
   - Install "python3-pip"
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
- This is where we run commands to automatically create the ELB instance that our application will run on
    - Follow the directions [here:](https://scribehow.com/shared/How_to_install_AWS_EB_CLI__J6eBRB9FQl2fGenfUVemlA)
- At the end of the an ELB instance is created for our application


### 4. Add the 'Deploy' stage to the Jenkins file in Jenkins
- In Jenkins
    - Open the Jenkinsfile.
	- Add the following 
	 - `stage ('Deploy') { steps { sh '/var/lib/jenkins/.local/bin/eb deploy' } }`
    - Rerun the build
- Observed the following:
    - The commits included in the Stage view
    - The deploy stage was added 	

### 5. If redeployed successfully to Elastic Beanstalk, what changed?
- When the application deployed again the following was updated:
    - Changes to GitHub were listed in Jenkins Status changes
    - The additional stage Deploy was added to the stage view
    - The Deploy stage activates a shell script that uploads the contents of the application '/var/lib/jenkins/.local/bin/' folder to the ELB instance. 

### 6. Configure a Webhook in Github
- In settings on the main repo page
    - Click 'Webhooks'
    - Add Webhook
    - In the Payload URL field enter
    	-`http:InstanceIP.com:Port#/github-webhook/`
    - Then Add Webhook to save
    - Next, you will need to check if it was configured correctly by selecting
    	- Recent Deliveries
     - [Webhooks](https://github.com/andmulLABS01/Deployment_3AM/blob/main/Webhooks.PNG)

### 7. BONUS: Once you've configured your webhook, change the background or some text in the application. 
- I modified the text in the home.html file on GitHub.

### 8. Did the application redeploy?
- Yes the application was redeployed and Jenkens pulled in the new commits on GitHub 
 - Followed the steps in the Jenkins file [HERE](https://github.com/andmulLABS01/Deployment_3AM/blob/main/StageView.PNG)
 - Deployed the updated information
    - [BEFORE](https://github.com/andmulLABS01/Deployment_3AM/blob/main/BeforeEdit.PNG)
    - [AFTER](https://github.com/andmulLABS01/Deployment_3AM/blob/main/AfterEdit.PNG)

## System Diagram:

To view the diagram of the system design/deployment pipeline, click [HERE](https://github.com/andmulLABS01/Deployment_3AM/blob/main/Depoyment3.drawio.png)

## Issues/Troubleshooting:


## Conclusion:

This deployment can be improved. One improvement would be to automate the creation of the following:
- AWS instance
- Jenkins server
- Creating AWS IAM Roles
- Installing the AWS CLI
- Creating the ELB instance

Some of the automation would include writing Bash scripts for the installation process and using Python to help automate the Server and ELB instances. We may also want to start thinking about how we will handle incident response if we need to roll back an application. Including which rollback strategies are appropriate for a given situation. 
