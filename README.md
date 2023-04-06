# Reto 3

En este reto teniamos que desplegar dos instancias de drupal que fueran proveidas por un balanceador de carga Apache y que usen una base de datos MariaDB y servidor de archivos NFS. También, debe estar el balanceador de carga debe estar connectado a un dominio y usar https para communicarse.

<img width="497" alt="Screen Shot 2023-04-06 at 11 22 28 AM" src="https://user-images.githubusercontent.com/28406146/230438896-e1d4a610-f476-43e7-9b3a-2dc982a74268.png">

## Crear EC2

Ve a AWS, entra a EC2, y hacele click a Launch instance. La instancia debe ser Ubuntu 22.22, cambia la llave de acceso, y deja el resto de las opciones por defecto.

Ahora ve a la instancia de EC2, ve a security y habilita los puertos que va usar esa instancia.(Lo puedes ver en el docker compose. También si es para haceso privado puedes usar una submascara privada para que solo puedan entrar las instancias privadas)

## Installar docker

Correr estos commandos para installar docker

```
sudo apt-get remove docker docker-engine docker.io containerd runc 
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo chmod a+r /etc/apt/keyrings/docker.gpg
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Descargar repositorio

Para descargar repositorio usa:

```
git clone https://github.com/amchp/reto3.git
```
