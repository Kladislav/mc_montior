# MC_MONITOR

Mediacube services montioring.

## Installation

### Install Docker

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt update
sudo apt install docker-ce
```
### Setting up  
```bash
git clone https://github.com/Kladislav/mc_montior
cd mc_monitor
cp .env.example .env
```
#### Configuring NGINX
#### Add to default_sever server directive
```
location /nginx_status {
    stub_status on;
    access_log off;
    allow 127.0.0.1;
    allow 172.22.0.1/24; //edit this
    deny all;
}
```
#### Add to your main server directive
```
location /grafana {
     access_log off;
     proxy_set_header   Host $host;
     proxy_pass http://127.0.0.1:$YOUR_GRAFANA_PORT;
     rewrite  ^/grafana/(.*)  /$1 break;
}
```

#### Configuring Postgres
```
host    all             all             172.22.0.0/24            trust
```

