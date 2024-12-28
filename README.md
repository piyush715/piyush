DevOps Practical
Things to Check Before Proceeding
Check That Git Is Installed in the System
Verify Installation:

git --version
If not installed, visit Git SCM and download.

Verify Java Installation:

java --version
Java version should be 8, 11, or 21.
If not installed, download and install Java, and set the path in environment variables:
JAVA_HOME
Paste the path of the bin folder of Java 8, 11, or 21.
Step 1: Setup Git Repository
Create a Folder: Save the Java code in the folder.
Initialize Git: Open Git Bash in the folder and run:
git init
Stage Java Files:
git add .
Commit Changes:
git commit -m "<any message>"
Link to Remote Repository:
Create a repository on GitHub.
Copy the repository link and run:
git remote add origin <paste link here>
Push to GitHub:
git push -u origin master
Or:
git push -u origin main
If any error occur use this commands:

echo "HELLO">README.md
git add .
git commit -m ""
git push -u origin main or master as per case
Step 2: Download and Setup Jenkins
For macOS:
Install Jenkins:
brew install jenkins-lts
Start Jenkins:
brew services start jenkins-lts
Access Jenkins: http://localhost:8080
Copy Password:
cat /usr/local/var/jenkins/home/secrets/initialAdminPassword
For Windows:
Download Jenkins:
Visit Jenkins Download Page.
Choose Windows and download the .msi installer.
Install Jenkins:
Follow the installation wizard.
Select "Install Suggested Plugins" when prompted.
Provide the path to your Java JDK.
Set the installation folder.
Configure the service port (default: 8080).
Retrieve Initial Password:
Navigate to:
C:\Program Files\Jenkins\secrets
Open the initialAdminPassword file and copy the password.
Step 3: Create a Jenkins Job
Open Jenkins: http://localhost:8080
Create a New Job:
Click on "New Item" in the dashboard.
Enter a job name.
Select "Freestyle Project" and click OK.
Configure the Job:
Go to the "Source Code Management" section.
Select "Git".
Enter the GitHub repository URL.
Choose the branch (main or master).
Build Trigger:
Check "Poll SCM" to let Jenkins check for changes.
In the schedule field, enter:
H/5 * * * *
Build Steps:
In the "Build" section, add a step:
For macOS: Select "Execute Shell".
For Windows: Select "Execute Windows batch command".
Enter commands to compile and run Java code:
javac <program_name>.java
java <program_name>
Save and Build the Job:
Click "Save".
Click "Build Now".
Verify the Build Output:
Go to "Build History".
Click on the build number and view the console output.
Step 4: Automate the Build
Configure Webhook in GitHub:

Go to the repository settings.
Navigate to "Webhooks" and click "Add webhook".
Set the Payload URL to:
http://localhost:8080/github-webhook/
Select "application/json" as content type.
Choose "Just the push event".
Install GitHub Integration Plugin in Jenkins:

Go to "Manage Jenkins > Manage Plugins".
Search for "GitHub Integration Plugin" and install it.
Update Jenkins Job Configuration:

Enable the "GitHub hook trigger for GITScm polling" option in the job configuration.
Test Automation:

Push changes to the GitHub repository.
Verify the new build is triggered in Jenkins.
Check the console output for successful build and execution.
Step 5: Deploy Application Locally
Create a Deployment Script:

For Windows (deploy.bat):
@echo off
echo Starting the HelloWorld application...
java <program name>
pause
For macOS (deploy.sh):
#!/bin/bash
echo "Starting the HelloWorld application..."
java <program name>
Test the Script:

Run the script locally.
Verify the application runs as expected.
Add the Script to Jenkins:

In Jenkins, navigate to the job configuration.
Add a new build step to execute the script:
Windows: deploy.bat
macOS:
chmod +x deploy.sh
./deploy.sh
Step 6: Test the Pipeline (CI/CD)
Make Changes to the Code:

Edit the Java file.
Save the changes.
Push Changes to the Repository:

git add <filename>
git commit -m "Updated message"
git push origin master
Observe Jenkins Automation:

Verify a new build is triggered automatically.
Check the console output for successful build and deployment.
Verify the Application:

Test the application locally.
For web services, test the local URL.
Troubleshoot Issues:

Check Jenkins console output for errors.
Verify environment setup and configurations.
