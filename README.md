# Quickstart

https://killercoda.com/playgrounds/scenario/kubernetes    

## Prepare

```
rm /usr/bin/helm && curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
mv /usr/local/bin/helm  /usr/bin/

```


https://gateway.envoyproxy.io/v0.5.0/user/quickstart/     



# Dev
https://killercoda.com/playgrounds/scenario/ubuntu    
 
```
wget https://go.dev/dl/go1.20.6.linux-amd64.tar.gz && rm -rf /usr/local/go && tar -C /usr/local -xzf go1.20.6.linux-amd64.tar.gz

```


```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg -y ; done

```

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

```
# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

```


```
apt-cache madison docker-ce | awk '{ print $3 }'
```

```
VERSION_STRING=5:20.10.16~3-0~ubuntu-focal
sudo apt-get install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-buildx-plugin docker-compose-plugin -y

```

```
git clone https://github.com/envoyproxy/gateway.git
```

```
make help
```


https://gateway.envoyproxy.io/v0.5.0/contributions/develop/    
https://docs.docker.com/engine/install/ubuntu/     

---

# EG

https://gateway.envoyproxy.io/v0.5.0/    










# envoyproxy-gateway



https://github.com/envoyproxy/gateway   


<img width="1651" alt="architecture" src="https://user-images.githubusercontent.com/13954225/233783791-3ec49a88-b58c-4b59-a38f-f1b094a85a08.png">
