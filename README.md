# MagentoDockerized

## Following the tutorial of https://github.com/markshust/docker-magento

### Execute the provided shell script to download the necessary files from Github
```
curl -s https://raw.githubusercontent.com/markshust/docker-magento/master/lib/template | bash
```

### Download the version of Magento you want to use with
```
bin/download 2.4.6-p3 community
```
### changes made for error encountered:

#### Could not connect to the Amqp Server.

#### changed the bin/setup command
```
  --amqp-host=rabbitmq \
  --amqp-port=5672 \
  --amqp-user=admin \
  --amqp-password=YjJiOTY0NDAxNWRkNmI1Y2Yx \
  --amqp-virtualhost=DSrabbitmq \
```
#### added the environment configuration in the docker image
```
  rabbitmq:
    image: rabbitmq:3.7-management-alpine
    ports:
      - "15672:15672"
      - "5672:5672"
    volumes:
      - rabbitmqdata:/var/lib/rabbitmq
    environment:
      - RABBITMQ_DEFAULT_USER=admin
      - RABBITMQ_DEFAULT_PASS=YjJiOTY0NDAxNWRkNmI1Y2Yx
      - RABBITMQ_DEFAULT_VHOST=DSrabbitmq
      - RABBITMQ_VM_MEMORY_HIGH_WATERMARK=1024MB
```

```
src: https://github.com/markshust/docker-magento/issues/426
```

### Run the setup installer for Magento:
```
bin/setup 127.0.0.1
```
### Open 127.0.0.1

### Note:

#### Need to enable Magento_TwoFactorAuth because
```
Cannot disable Magento_TwoFactorAuth because modules depend on it:
Magento_AdminAdobeImsTwoFactorAuth: Magento_AdminAdobeImsTwoFactorAuth->Magento_TwoFactorAuth
```

```
Open Mailcatcher 127.0.0.1:1080/ to configure Magento_TwoFactorAuth
```

#### App is in 
```
docker exec -it docker-magento2-app-1 sh
```

#### or
```
src folder
```

#### DB
```
User: magento
Password: magento
```
#### /admin
```
MAGENTO_ADMIN_USER=john.smith
MAGENTO_ADMIN_PASSWORD=password123
```
#### start/stop
```
docker-compose start
docker-compose stop
```
