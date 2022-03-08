# Docker Wordpress

Fast Development enviroment for Wordpress using docker

## Wordpress User
```
User: root
pass: root
email: root@mail.com
```

## How to

Start server
```bash
docker-compose up
```

Stop server
```bash
docker-compose stop
```

Delete container
```bash
docker-compose rm
```

## Themes files
Theme files in `wp-content/themes`

## Plugins files
Plugins files in `wp-content/plugins`

## Database files
Dababase files in `data`

## Throubleshooting

### Downloading Wordpress Failure 

Wordpress image tries download latest Wordpress and install it in container.
Sometimes this action fail for this causes:

* Internet connection error
* Server doesn't respond

**Solution:** Enter to container shell and try download wordpress manually.
```bash
docker-compose exec wordpress /bin/bash
wp core download
```

### Files permissions

Docker container is owner of files in `themes`, `plugins` and `database` files. It causes permission error when edit files is needed.

**Solution:** Change files permission for these folders
```bash
sudo chmod -R 777 data
sudo chmod -R 777 wp-content
```

### Wordpress is extremelly slow in page load
As Mac and Windows use a different filesystem to manage files this cause bottleneck in when data from shared folder is required.

Try with this way to load volumes.

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

 

