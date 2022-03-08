# Docker Wordpress

Permite levantar Wordpress rápidamente con Docker

## Usuario Wordpress
```
User: root
pass: root
email: root@mail.com
```
Si se parte con una versión limpia utilizar estas credenciales para estándarizar. 

## How to

Levantar el servidor

```bash
docker-compose up
```

Detener el servidor

```bash
docker-compose stop
```
Eliminar el contenedor

```bash
docker-compose rm
```


## Errores conocidos (Throubleshooting)

### Falla en la instalación de Wordpress
Cuando falla la conexión con el instalador de wordpress en necesario descargarlo manualmente:
```bash
docker-compose exec wordpress /bin/bash
wp core download
```

### Permisos 
Como docker escribe en los archivos cambia los permisos.
Simplemente otorgar todos los permisos ayuda.
```bash
sudo chmod -R 777 data
sudo chmod -R 777 wp-content
```

### En caso de lentitud

Es posible que sistemas Windows y Mac haya lentitud cuando se comparten archivos del proyecto mediante volumenes, debido a la diferencias entre los sistemas de archivos.

Probar esta forma de montar volumenes.

```yaml
volumes:
  - ./data:/data
  - ./scripts:/docker-entrypoint-initwp.d
  #- ./wp-content:/app/wp-content
  - type: bind
    source: ./wp-content
    target: /app/wp-content
    consistency: cached
  #- ./php-conf:/usr/local/etc/php
  - type: bind
    source: ./php-conf
    target: /usr/local/etc/php
    consistency: cached
```

 

