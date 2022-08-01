# ELK_stack
Развертывание связки ELK(Elasticsearch + Logstash + Kibana) докер контейнеров с помощью ansible

Заменить inventory на свой.

Стандартный пароль пользователей elastic и kibana_system: pass. Пароли можно поменять в group_vars/all.yml. 

Для запуска использовать:
ansible-playbook -i inventory elk.yml -K

Для запуска на локальной машине добавить --extra-vars="ansible_connection=local"

Получить токен:
docker exec -it elasticsearch /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana

Получить код верификации kibana:
docker exec -it kibana kibana-verification-code 

Получить токен используя ansible:
ansible-playbook -i inventory get_secrets.yml -t elastic --extra-vars="ansible_connection=local"

Получить код верификации kibana используя ansible:
ansible-playbook -i inventory get_secrets.yml -t kibana --extra-vars="ansible_connection=local"
