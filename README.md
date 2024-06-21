<strong>Project Overview</strong><br>
<strong>Objective</strong>: Deploy a simple website using automation tools.<br>
<strong>Skills Practiced</strong>: Infrastructure setup, coding, scripting, automation.<br>

<strong>Prerequisites</strong>
Basic knowledge of web development (HTML, CSS, JavaScript)
Familiarity with server deployment (e.g., using AWS EC2)
Understanding of networking concepts
Basic knowledge of Terraform, Ansible, and Git
Steps to Complete the Project.<br>

Step 1: Set Up Version Control with GitHub
Create a GitHub repository for your project.
Clone the repository to your local machine.
<br>

git clone https://github.com/your-username/simple-website-devops.git
cd simple-website-devops
<br>
Step 2: Develop a Simple Website
Create the website files (index.html, styles.css, script.js) in your repository.
Commit the website files to your repository.
<br>

git add .
git commit -m "Add simple website files"
git push origin main
<br>

Step 3: Set Up Infrastructure with Terraform
Install Terraform if you haven't already.

Create Terraform configuration (main.tf and provider.tf files) files to provision an AWS EC2 instance.
Initialize Terraform and apply the configuration.
<br>

terraform init
terraform apply

Note the public IP address of the EC2 instance from the Terraform output.
<br>
Step 4: Automate Deployment with Ansible
Install Ansible if you haven't already.

Create an Ansible playbook to deploy the website files to the EC2 instance.

[web]
<INSTANCE_IP> ansible_user=ec2-user ansible_ssh_private_key_file=~/.ssh/your_key.pem
site.yml:

yaml
Copy code
- hosts: web
  tasks:
    - name: Install Git
      yum:
        name: git
        state: present

    - name: Clone the website repository
      git:
        repo: https://github.com/your-username/simple-website-devops.git
        dest: /var/www/html
        version: main
Run the Ansible playbook to deploy the website.
<br>

ansible-playbook -i hosts.ini site.yml
Step 5: Verify the Deployment
Access the website by navigating to the public IP address of your EC2 instance in a web browser.
<br>

http://<INSTANCE_IP>
You should see the simple website with the message "Welcome to My Simple Website."

<strong>Conclusion</strong>
This project involves:
Creating a simple website with HTML, CSS, and JavaScript.
Using GitHub for version control.
Setting up an EC2 instance with Terraform.
Automating the deployment of the website using Ansible.