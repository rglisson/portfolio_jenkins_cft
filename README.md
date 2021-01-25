# Jenkins AWS Demo

![](images/jenkins.PNG)

# Introduction & Goals
- The goal of the project was to use Jenkins to assist in CI/CD to automatically deploy a new cloudformation stack when there was a new commit on a github repo.

# Tools Used
- Jenkins
- CloudFormation
- S3
- Systems Manager

# Process
- Create a Role for EC2. We'll give this role access to S3, CloudFormation, and Systems Manager so that we don't have to worry about using access keys.

![](images/role-1.PNG)

![](images/ssm.PNG)

![](images/ssm-2.PNG)

- Create a new EC2. I'm using a AWS linux EC2 t2 micro instance.

![](images/linux-ec2.PNG)

- In the security group, add port 8080.

![](images/sg.PNG)

- I downloaded Jenkins onto this instance using the template from this link: https://www.jenkins.io/doc/book/installing/linux/#red-hat-centos. Once installed, run Jenkins:
  - sudo systemctl start jenkins
  - sudo systemctl status jenkins
  - sudo systemctl stop jenkins

- Copy the public IPv4 address and add :8080 on the end of the URL

- Once loggedin, add the jenkins-cloudformation-plugin

![](images/plugin.PNG)

- Create a new pipeline build 

![](images/build1.PNG)

- Choose 'github hook trigger'

![](images/hook.PNG)

- Connect the github repo by pasting the URL and adding credentials

![](images/git.PNG)

- Type the jenkins file name, which I have under 'jenkinsfile' in my repo

![](images/jenkinsfile.PNG)

![](images/jenkinsfile-1.PNG)

- Here's the cloudformation JSON script. This will simply add a new S3 bucket.

![](images/cft.PNG)

- In order to trigger new commits to the pipeline, in github go to settings, webhooks, and add the following:

![](images/webhook-1.PNG)


- Now, whenever we make a new commit, jenkins runs a new build immediately. 

![](images/push-1.PNG)

![](images/push-2.PNG)

- Output of CloudFormation stack:

![](images/push-3.PNG)

- Output of S3 bucket:

![](images/push-4.PNG)

- Jenkins pipeline UI

![](images/push-5.PNG)


# Conclusion
- Jenkins is a universal automation software tool. Once configured on AWS, you can configure your CI/CD pipelines. In this case I downloaded a CloudFormation plugin to automatically deploy my infrastructure-as-code everytime I make a new commit on my github repo.
