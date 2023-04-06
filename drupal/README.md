# Servidor backend Drupal

## Crear EC2, installar docker y descargar repositorio

Hay un README.md justo afuera de este folder que muestra como crear una EC2, installar docker y descargar el repositorio. También, es recomendado tener primero el servidor nfs porque este guarda los archivos de Drupal.

## Montar nfs

Para tener los archivos de Drupal hay que montar el servidor nfs en el folder de drupal lo haces con estos commandos.

```
mkdir nfs
sudo mount -t nfs <IP privada nfs>:/exports ./nfs
```

## Cambiar archivo de configuración

Hay que cambiar unos valores de archivo de configuración que lo puedes encontrar en "./nfs/sites/default/settings.php".

Hay que cambiar la conneción a la base de datos.

```
$databases['default']['default'] = array (
  'database' => <nombre de base de datos>,
  'username' => <nombre de usuario>,
  'password' => <clave de usuario>,
  'prefix' => '',
  'host' => <IP privada de base de datos>,
  'port' => '3306',
  'namespace' => 'Drupal\\mysql\\Driver\\Database\\mysql',
  'driver' => 'mysql',
  'autoload' => 'core/modules/mysql/src/Driver/Database/mysql/',
);
```

También hay que cambiar la IP del balanceador de carga.

```
$settings['reverse_proxy_addresses'] = ['<IP privada de balanceador de carga>'];
```

## Correr Drupal

Ya solo tienes que correr.

```
sudo docker compose up
```

y debería empezar el backend de Drupal.