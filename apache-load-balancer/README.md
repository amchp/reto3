# Balanceador de Carga

## Crear EC2, installar docker y descargar repositorio

Hay un README.md justo afuera de este folder que muestra como crear una EC2, installar docker y descargar el repositorio.

## Modificar configuración

Tienes que cambiar varias secciones de la configuración.

Primero, empecemos con el archivo principal de configuración httpd.conf.
Empieza cambiando el proxy.

```
<Proxy "balancer://mycluster">
    BalancerMember "<dominio privado servidor backend>"
    BalancerMember "<dominio privado servidor backend>"
</Proxy>
```

Cambia el host:

```
RequestHeader set Host "<dominio publico>"
```

Por último cambia lo que pasa las galletas:

```
ProxyPassReverseCookieDomain "<dominio privado servidor backend>" "<dominio publico>"
ProxyPassReverseCookieDomain "<dominio privado servidor backend>" "<dominio publico>"
```

En el http-ssl.conf solo tienes que cambiar el nombre del servidor.

```
ServerName <dominio publico>
```

## Crear certificado de SSL

Debemos crear un certificado ssl para tu dominio.

```
sudo certbot certonly --apache -d <dominio>
```

Llena la información que te pide y el commando y al final te dara un certificado de tu dominio.

Busca el certificado de tu dominio y copiarlo al folder donde tienes todo lo del balanceador de carga y cambia el archivo de docker compose para que usen los certificados que copiaste.

Estas dos lineas.
```
- ./<certificado>:/usr/local/apache2/conf/fullchain.pem
- ./<llave privada>:/usr/local/apache2/conf/privkey.pem
```

## Correr Balanceador de Carga

Ya solo tienes que correr.

```
sudo docker compose up
```

y debería empezar el balanceador de carga.
