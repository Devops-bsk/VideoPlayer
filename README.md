## Build and Deploy a Modern Video Player Application in React JS with Material UI 5


****1.Writing Terraform for Jenkins , Docker and SonarQube server**
resource "aws_instance" "ec2" {
  ami = "ami-06c4be2792f419b7b"
  key_name = "Singapore"
  instance_type = "t2.large"
    vpc_security_group_ids = [aws_security_group.Jenkins-vm-sg.id]
    user_data = templatefile("./install.sh" , {})
     

    tags = {
      Name = "Jenkins-sonar"
    }
    root_block_device {
      volume_size = 40
    }
}

resource "aws_security_group" "Jenkins-vm-sg" {
    name = "Jenkins-vm-sg"
    description = "Allows TLS inbound traffic"
    ingress = [
        for port in [22,80,443,3000,9000,8080] : {
            description = "inbound rules"
            from_port = port
            to_port = port
            protocol = "tcp"
            cidr_blocks = ["0.0.0.0/0"]
            ipv6_cidr_blocks = []
            prefix_list_ids = []
            security_groups = []
            self = false
        }
    ]
    egress  {
        from_port = 0
        to_port = 0
        protocol = -1
        cidr_blocks = ["0.0.0.0/0"]
        
    }
    tags = {
      Name = "Jenkins-vm-sg"
    }

}


**2.Configure Jenkins**


**3.Configure sonarQube and Integrate SonarQube with Jenkins**


**4.Create Jenkins Pipeline to build and push Docker Image to DockerHub**


**5.Create EC2 & Setup for Prometheus and Grafana**
resource "aws_instance" "monitor" {
    ami = "ami-06c4be2792f419b7b"
    instance_type = "t2.medium"
    key_name = "Singapore"
    vpc_security_group_ids = [aws_security_group.MySecurity.id]
    user_data = templatefile("./install.sh", {})
    
tags = {
  Name = "Monitoring-server"
}
root_block_device {
  volume_size = 20
}
  
}
resource "aws_security_group" "MySecurity" {
    name = "Monitoring_SG"
    description = "This is for monitoring"
    ingress = [
        for port in [22,80,443,9090,3000,9100] : {
            description = "inbound rules"
            from_port = port
            to_port = port
            protocol = "tcp"
            cidr_blocks = ["0.0.0.0/0"]
            ipv6_cidr_blocks = []
            prefix_list_ids = []
            security_groups = []

            self = false
        }
    ]

egress {
    from_port = 0
    to_port = 0
    protocol = "-1"
    cidr_blocks = ["0.0.0.0/0"]

}
tags = {
  Name = "Monitoring-server-SG"
}
  
}

**6.Setup Email Notification through Jenkins**


**7.Create AWS EKS Cluster**


**8.Integrate Prometheus with EKS and Import Grafana Monitoring Dashboard for K8s**



**9.Configure the Jenkins pipeline to deploy Application on AWS EKS**



**10.Set trigger and verify CI/CD pipeline**


