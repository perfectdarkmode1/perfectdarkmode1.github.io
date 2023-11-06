```
title: "Calibre Web with Docker Setup"
date: 2023-11-06T06:20:36-07:00
draft: false
```
```sh
cd ~/Documents
rsync -avuP your-library-dir root@example.org:/opt/calibre/
```

1. Install Docker
```
sudo apt update
sudo apt install docker.io
```

2. Create a Docker Network
```
dthomas@david2:/etc/systemd/system$ sudo docker network create calibre_network
556a9ca12eafd36768f068d3de071d357870a145c4ccc400c601819d420040cf
```

3. Create a Docker volume to store Calibre Web data:
```
sudo docker volume create calibre_data
```

4. Pull the Calibre Web Docker image:
```
sudo docker pull linuxserver/calibre-web
```

5. Start the Calibre Web Docker container
```sh
sudo docker run -d \ 
--name=calibre-web \ 
--restart=unless-stopped \ 
-p 8083:8083 \ 
-e PUID=$(id -u) \ 
-e PGID=$(id -g) \ 
-v calibre_data:/config \ 
-v /opt/calibre/Calibre:/books \ 
--network calibre_network \ 
linuxserver/calibre-web
```

6. Configure Nginx to act as a reverse proxy for Calibre Web:
```
sudo nano /etc/nginx/sites-available/calibre-web
```

Add the following to the file
```
server { listen 80; server_name example.com; # Replace with your domain or server IP location / { proxy_pass http://localhost:8083; proxy_set_header Host $host; proxy_set_header X-Real-IP $remote_addr; proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; proxy_set_header X-Forwarded-Proto $scheme; } }
```

Enable the site
```
sudo ln -s /etc/nginx/sites-available/calibre-web /etc/nginx/sites-enabled/
```

Test the configuration
```
sudo nginx -t
```

Restart nginx

```
sudo service nginx restart
```

Set up a cname record for your site with your DNS provider
```
calibre.example.com
```

Install ssl cert using certbot
```
certbot --nginx
```

Heat to the site at https://calibre.example.com

login with default credentials

username: admin
password: admin123

select /books as the library directory. Go into admin settings and change your password. 

Whenever you add new books to your server via rsync, you will need to restart the Calibre Web Docker container:

```
sudo docker restart calibre-web
```

Then restart nginx

```
systemctl restart nginx
```