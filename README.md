# CI/CD django-docker-jenkins-ansible guide project

Continous Delivery is a simple process thanks to the tools developed over the years. This repo aims to provide template for developers and engineers to avoid the tedious manual software delivery process. The approach taken utilizes Django, Docker, Jenkins and Ansible.

## Getting started
This project works well with a Trunk-based workflow and requires the following:
* Docker
* Docker Compose
* Jenkins
* Python
* Django 
* Github

### Setting up a testing pipeline on Jenkins
1. Log into Jenkins and Click on **New Item**.
2. Fill the **Enter an item name** form field.
3. Select the **Multibranch Pipeline** option and Click Ok.
4. On the **General tab**, fill in the **name** and **description** form fields.
5. Now click the **add source** button on the **Branch sources** tab and select **Github**.
6. Add/Select Github credentials.
7. Fill the **Repository HTTPS URL** field with the your github repo URL.
8. Move to the **Build Configuration** tab and select **Mode** to be **by Jenkinsfile**.
9. Fill the path to the Jenkins file on your repo in the **Script path** field.
10. Lastly, check the **Discard old items** option and click **Save**.

## License
TODO

## Consulting
My name is Bonface Thaa, I am a software consultant, engineer and a tech lead. I work on technologies trends that shape the future, particularly in web, data and devops. Need some help with any tools used in this repo? Inbox me @ thaabonface@gmail.com and lets deliver your product!
