# This is my own template for docker compose
I used podman as container management-tool. So, the first step is you need to install podman-compose.

## Install Podman Compose
make sure you have pip installed in your machine
```
pip --version
```

output :
```
pip 22.2.1 from C:\xxx\Python310\lib\site-packages\pip (python 3.10)
```

after that, you can continue installed podman-compose
```
pip install podman-compose
```

## Generate container one-by-one
### Podman Compose DB
```
podman-compose -f ./docker-compose-db.yml up -d
```
### Podman Compose Kafka and Zookeper
```
podman-compose -f ./docker-compose-kafka.yml up -d
```
### Podman Compose Consul and Vault
```
podman-compose -f ./docker-compose-consul-vault.yml up -d
```