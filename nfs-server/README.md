# Servidor NFS

## Crear EC2, installar docker y descargar repositorio

Hay un README.md justo afuera de este folder que muestra como crear una EC2, installar docker y descargar el repositorio.

## Cambiar permisos de folders

Hay que cambiar los permisos para qe cualquier usuario pueda escribir en los folders excepto en los archivos de configuración.

```
chmod -R 777 exports
chmod 755 exports/sites/default/settings.php
chmod 755 exports/sites/default/default.settings.php
```

## Poner kernel NFS

Cada vez que inicie la maquina tienes que correr este commando para que en el kernel inicie nfs

```
sudo modprobe nfs
sudo modprobe nfsd
```

## Correr Servidor NFS

Ya solo tienes que correr.

```
sudo docker compose up
```

y debería empezar el servidor NFS.