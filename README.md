provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "EC1" {
  ami             = "ami-0ae69fd56f71576ad"
  instance_type   = "t2.micro"
  key_name        = "DevOps_complete_Project"
  vpc_security_group_ids = [aws_security_group.SG_project1.id] # Use `id` for VPC

  tags = {
    Name = "EC1"
  }
}

/* Creation of the SG */

resource "aws_security_group" "SG_project1" {
  name        = "SG_project1"
  description = "Allow inbound traffic for SSH connection"

  tags = {
    Name = "SG_project1"
  }

  ingress {
    description = "SSH access"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    description = "Allow all outbound traffic"
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
