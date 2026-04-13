# 03-ec2-nginx-foundations

## Objective

Launch a small EC2 instance, connect through SSH, install Nginx, validate the service locally and externally, and clean up the resource correctly.

## Why this matters in real-world DevOps

EC2 is a core AWS compute service. A DevOps engineer must understand how to launch an instance with minimal exposure, validate access, install and operate a service, expose only the required port, confirm the request path through logs, and clean up the resource after the lab.

## Scope

This lab covered:

- EC2 launch with Amazon Linux 2023
- small instance sizing for a simple service workload
- SSH access using a key pair
- Security Group with minimal initial exposure
- Nginx installation and service management
- local validation before external exposure
- HTTP exposure through Security Group update
- external validation by public IP
- Nginx access and error log review
- resource cleanup

## Instance design

- Name: `s2-ec2-nginx-lab-01`
- AMI: Amazon Linux 2023
- Instance type: `t3.small`
- SSH: allowed only from current public IP
- HTTP: opened only after local service validation
- HTTPS: not opened
- Tags:
  - `Project=DevOpsDublin2026`
  - `Sprint=2`
  - `Env=lab`
  - `Owner=pablogs04`
  - `ManagedBy=manual`

## Commands used

```bash
hostnamectl
whoami
uptime
df -h
sudo dnf update
sudo dnf install -y nginx
sudo systemctl start nginx
sudo systemctl enable nginx
systemctl is-active nginx
sudo ss -lntp | grep ':80 '
curl -I http://localhost
sudo systemctl status nginx --no-pager
sudo tail -n 20 /var/log/nginx/access.log
sudo tail -n 20 /var/log/nginx/error.log