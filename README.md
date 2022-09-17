# docker-phpmyadmin

## install docker
```bash
sudo yum update -y
sudo yum install docker git -y
sudo usermod -a -G docker ec2-user
```
restart the session to able to run docker commands

## install docker compose
```bash
wget https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) 
sudo mv docker-compose-$(uname -s)-$(uname -m) /usr/local/bin/docker-compose
sudo chmod -v +x /usr/local/bin/docker-compose
echo "$PATH"
export PATH=$PATH:/usr/local/bin
```

## start docker service
```bash
sudo systemctl enable --now docker.service
```

## configure caddy
```bash
cp Caddyfile-sample Caddyfile
```

```
host.domain.tld {
  reverse_proxy <CONTAINER>:<PORT>
  reverse_proxy /<DIR>/<PATH> <CONTAINER>:<PORT>
}
```

## configure env
```bash
cp .env-example .env
```

```
PMA_ARBITRARY=1
PMA_ABSOLUTE_URI=https://host.domain.tld
```

## start phpmyadmin
```bash
docker-compose up -d
```