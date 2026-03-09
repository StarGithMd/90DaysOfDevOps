## Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## Today's goal is to deploy a real web server on the cloud and learn practical server management.

## 1. Launch a Cloud Instance
 - AWS EC2: Go to the AWS Management Console → EC2 → Launch Instance. Choose an OS (Ubuntu is common), select instance type, configure storage, and launch

# ssh -i your-key.pem ubuntu@100.48.71.111
# curl ifconfig.me
100.48.71.111

# sudo apt update-y; apt upgrade -y

# apt install nginx -y
# systemctl start nginx
# systemctl enable nginx
# systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: en>
     Active: active (running) since Mon 2026-03-09 17:54:19 UTC; 38s ago
       Docs: man:nginx(8)
    Process: 14633 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_proc>
    Process: 14635 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (>
   Main PID: 14665 (nginx)
      Tasks: 3 (limit: 1008)
     Memory: 2.4M (peak: 5.3M)
        CPU: 29ms
     CGroup: /system.slice/nginx.service

## Configure Security Groups: In AWS EC2 or Utho, edit the security group attached to your instance

- Add an Inbound Rule:
- Type: HTTP
- Port: 80
- Source: 0.0.0.0/0 (for public access)

## Verify Webpage Accessibility
# curl http://100.48.71.111
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>


## Extract and Save Log
# cp /var/log/nginx/access.log ~/nginx_access.log

# cat nginx_access.log
103.50.150.115 - - [09/Mar/2026:18:04:57 +0000] "GET / HTTP/1.1" 200 409 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/145.0.0.0 Safari/537.36 Edg/145.0.0.0"
103.50.150.115 - - [09/Mar/2026:18:04:58 +0000] "GET /favicon.ico HTTP/1.1" 404 196 "http://100.48.71.111/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/145.0.0.0 Safari/537.36 Edg/145.0.0.0"
100.48.71.111 - - [09/Mar/2026:18:05:15 +0000] "GET / HTTP/1.1" 200 615 "-" "curl/8.5.0"
100.48.71.111 - - [09/Mar/2026:18:06:04 +0000] "GET / HTTP/1.1" 200 615 "-" "curl/8.5.0"


## Verify Webpage Accessibility

- Open a browser and enter your instance’s public IP.
A. this is able to accessib;e the default page of nginx
- You should see the default Nginx welcome page: “Welcome to Nginx!”.
A. Welcome to nginx!
If you see this page, the nginx web server is successfully installed and working. Further configuration is required.

For online documentation and support please refer to nginx.org.
Commercial support is available at nginx.com.

Thank you for using nginx.

- If not, double‑check:
- Nginx service status: sudo systemctl status nginx
# systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: en>
     Active: active (running) since Mon 2026-03-09 17:54:19 UTC; 16min ago
       Docs: man:nginx(8)
    Process: 14633 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_proc>
    Process: 14635 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (>
   Main PID: 14665 (nginx)
      Tasks: 3 (limit: 1008)
     Memory: 2.4M (peak: 5.3M)
        CPU: 31ms
     CGroup: /system.slice/nginx.service

- Security group rules
- sgr-0685a9a2b65f62240	443	TCP		0.0.0.0/0	launch-wizard-1 
– sgr-0adb02b35d838ac7f	80	TCP		0.0.0.0/0	launch-wizard-1 

- Firewall settings (if applicable)
