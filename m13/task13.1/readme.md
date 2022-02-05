Install and configure infrastructure as a Code using Terraform:
```

resource "aws_vpc" "mainvpc" {
  cidr_block = "10.0.0.0/16"
}
resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.mainvpc.id
}

resource "aws_route_table" "toGateway" {
  vpc_id = aws_vpc.mainvpc.id
  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.gw.id
  }
}
resource "aws_route_table_association" "a" {
  subnet_id      = aws_subnet.SubnetPublic.id
  route_table_id = aws_route_table.toGateway.id
}

//--------------SUBNETS--------------------------------
resource "aws_subnet" "SubnetPublic" {
  vpc_id                  = aws_vpc.mainvpc.id
  cidr_block              = "10.0.10.0/24"
  availability_zone       = "eu-central-1c"
  map_public_ip_on_launch = true
  tags = {
    Name = "SubnetPublic"
  }
}
resource "aws_subnet" "SubnetPublic2" {
  vpc_id                  = aws_vpc.mainvpc.id
  cidr_block              = "10.0.11.0/24"
  availability_zone       = "eu-central-1b"
  map_public_ip_on_launch = true
  tags = {
    Name = "SubnetPublic2"
  }
}
resource "aws_subnet" "SubnetPrivate" {
  vpc_id     = aws_vpc.mainvpc.id
  cidr_block = "10.0.2.0/24"
  //  map_public_ip_on_launch = true
  tags = {
    Name = "SubnetPrivate"
  }
}
resource "aws_subnet" "SubnetDB1" {
  vpc_id            = aws_vpc.mainvpc.id
  availability_zone = "eu-central-1a"
  cidr_block        = "10.0.30.0/24"
  tags = {
    Name = "SubnetDB1"
  }
}
resource "aws_subnet" "SubnetDB2" {
  vpc_id            = aws_vpc.mainvpc.id
  availability_zone = "eu-central-1b"
  cidr_block        = "10.0.31.0/24"
  tags = {
    Name = "SubnetDB2"
  }
}
//---------------------------------------------------
/*
resource "aws_lb" "ALB" {
  name                       = "test-lb"
  internal                   = false
  load_balancer_type         = "application"
  security_groups            = [aws_security_group.myHTTP.id]
  subnets                    = [aws_subnet.SubnetPublic.id, aws_subnet.SubnetPublic2.id]
  enable_deletion_protection = false
}
resource "aws_lb_target_group" "ALBtarget" {
  name = "tf-example-lb-tg"
  port = 80
  //  health_check = false
  protocol    = "HTTP"
  vpc_id      = aws_vpc.mainvpc.id
  target_type = "instance"
}

resource "aws_lb_target_group_attachment" "ALBtarget1" {
  target_group_arn = aws_lb_target_group.ALBtarget.arn
  target_id        = aws_instance.my_frontend.id
  port             = 80
}

resource "aws_alb_listener" "myALBlistener" {
  load_balancer_arn = aws_lb.ALB.arn
  port              = "80"
  protocol          = "HTTP"
  default_action {
    type             = "forward"
    target_group_arn = aws_lb_target_group.ALBtarget.arn
  }
}
*/
//--------------SG--------------------------------

resource "aws_security_group" "myHTTP" {
  name   = "myHTTP"
  vpc_id = aws_vpc.mainvpc.id

  ingress {
    description = "incoming http"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
  }
  ingress {
    description = "incoming http"
    from_port   = 8
    to_port     = 0
    protocol    = "icmp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port        = 8
    to_port          = 0
    protocol         = "icmp"
    cidr_blocks      = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
  }
  tags = {
    Name = "myHTTP"
  }
}

resource "aws_security_group" "BastionSSH" {
  name        = "SSH"
  description = "SSHonly"
  vpc_id      = aws_vpc.mainvpc.id
  //  lifecycle { create_before_destroy = true }

  ingress {
    description = "incoming SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
  }
  tags = {
    Name = "SSH"
  }
}

resource "aws_security_group" "dbSQL" {
  name        = "SQL"
  description = "SQL"
  vpc_id      = aws_vpc.mainvpc.id
  //  lifecycle { create_before_destroy = true }

  ingress {
    description = "incoming sql"
    from_port   = 3306
    to_port     = 3306
    protocol    = "tcp"
    cidr_blocks = ["10.0.0.0/16"]
  }

  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
  }
  tags = {
    Name = "MySQL"
  }
}

resource "aws_db_subnet_group" "dbSQLsubnetGroup" {
  name       = "sqlsubnetgroup"
  subnet_ids = [aws_subnet.SubnetDB1.id, aws_subnet.SubnetDB2.id]

  tags = {
    Name = "DB subnet group"
  }
}

//--------------Instance--------------------------------
/*
resource "aws_instance" "Bastion" {
  //  count                  = 0
  ami                    = "ami-0453cb7b5f2b7fca2"
  instance_type          = "t2.micro"
  vpc_security_group_ids = [aws_security_group.BastionSSH.id]
  subnet_id              = aws_subnet.SubnetPublic.id
  user_data              = file("proj1.sh")
  key_name               = "Victor-key-frankfurt"
  //depends_on =
  tags = {
    Name = "myBastion"
  }
}
///*
resource "aws_instance" "my_frontend" {
  //  count                  = 0
  ami                    = "ami-0453cb7b5f2b7fca2"
  instance_type          = "t2.micro"
  vpc_security_group_ids = [aws_security_group.BastionSSH.id, aws_security_group.myHTTP.id]
  subnet_id              = aws_subnet.SubnetPrivate.id
  user_data              = file("proj1.sh")
  key_name               = "Victor-key-frankfurt"
  tags = {
    Name = "Frontend"
  }
}

resource "aws_instance" "my_backend" {
  ami                    = "ami-0453cb7b5f2b7fca2"
  instance_type          = "t2.micro"
  vpc_security_group_ids = [aws_security_group.BastionSSH.id]
  subnet_id              = aws_subnet.SubnetPrivate.id
  user_data              = file("proj1.sh")
  key_name               = "Victor-key-frankfurt"
  tags = {
    Name = "Backend"
  }
}



//*/
```

Manually install jenkins:
```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
  
Then add a Jenkins apt repository entry:
    
  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
  
Update your local package index, then finally install Jenkins:
   
  sudo apt-get update
  sudo apt-get install jenkins
```
scp -v -o StrictHostKeyChecking=no index.html student@192.168.88.211:/var/www/html
Wehavetocopyid_rsato/var/lib/jenkins/.ssh
3)The/var/lib/jenkins/.sshdirectoryandfilesinsideofitshouldbeownedbyjenkins
