<strong>Project Overview</strong><br>
<strong>Objective</strong>: Deploy a simple website using automation tools.<br>
<strong>Skills Practiced</strong>: Infrastructure setup, coding, scripting, automation.<br>

<strong>Prerequisites</strong>
Basic knowledge of web development (HTML, CSS, JavaScript)
Familiarity with server deployment (e.g., using AWS EC2)
Understanding of networking concepts
Basic knowledge of Terraform, Ansible, and Git
Steps to Complete the Project
Step 1: Set Up Version Control with GitHub
Create a GitHub repository for your project.
Clone the repository to your local machine.
<br>
Copy code
git clone https://github.com/your-username/simple-website-devops.git
cd simple-website-devops
<br>
Step 2: Develop a Simple Website
Create the website files (index.html, styles.css, script.js) in your repository.
index.html:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Website</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Welcome to My Simple Website</h1>
    <p>This is a simple website deployed using DevOps practices.</p>
    <script src="script.js"></script>
</body>
</html>
<br>
styles.css:
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin-top: 50px;
}
<br>

script.js:
console.log("Website loaded successfully");
Commit the website files to your repository.
<br>

git add .
git commit -m "Add simple website files"
git push origin main
<br>

Step 3: Set Up Infrastructure with Terraform
Install Terraform if you haven't already.

Create Terraform configuration files to provision an AWS EC2 instance.

main.tf:
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2 AMI
  instance_type = "t2.micro"

  tags = {
    Name = "SimpleWebsite"
  }

  user_data = <<-EOF
              #!/bin/bash
              yum update -y
              yum install -y httpd
              systemctl start httpd
              systemctl enable httpd
              EOF
}

output "instance_ip" {
  value = aws_instance.web.public_ip
}
Initialize Terraform and apply the configuration.
<br>

terraform init
terraform apply

Note the public IP address of the EC2 instance from the Terraform output.
Step 4: Automate Deployment with Ansible
Install Ansible if you haven't already.

Create an Ansible playbook to deploy the website files to the EC2 instance.

hosts.ini:
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