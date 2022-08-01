# ELK_stack
## Развертывание связки ELK(Elasticsearch + Logstash + Kibana) докер контейнеров с помощью ansible

## Требования:
Наличие ansible и python.

В inventory нужно заменить ansible_host и ansible_user на своих.


## Стандартный пароль для пользователей elastic и kibana_system: pass. 

Пароли можно поменять в group_vars/all.yml. 

## Запуск

Для запуска использовать:
ansible-playbook -i inventory elk.yml -K

Для запуска на локальной машине добавить --extra-vars="ansible_connection=local"

## Токен и код верификации

### Используя Docker
Получить enrollment token:
docker exec -it elasticsearch /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana

Получить код верификации kibana:
docker exec -it kibana kibana-verification-code 

### Используя Ansible

Получить токен используя ansible:
ansible-playbook -i inventory get_secrets.yml -t elastic --extra-vars="ansible_connection=local"

Получить код верификации kibana используя ansible:
ansible-playbook -i inventory get_secrets.yml -t kibana --extra-vars="ansible_connection=local"
