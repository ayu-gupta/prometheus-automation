# Ansible Role: Prometheus Exporters
An ansible role which contains multiple exporters of prometheus for scrapping data and for enhancing your monitoring stack. Here are the list of exporters which we are supporting in this role:-
- **[Apache Exporter](https://github.com/Lusitaniae/apache_exporter)**
- **[Elasticsearch Exporter](https://github.com/justwatchcom/elasticsearch_exporter)**
- **[Kafka Exporter](https://github.com/danielqsj/kafka_exporter)**
- **[MongoDB Exporter](https://github.com/dcu/mongodb_exporter)**
- **[MySQL Exporter](https://github.com/prometheus/mysqld_exporter)**
- **[Nginx Exporter](https://github.com/nginxinc/nginx-prometheus-exporter)**
- **[Node Exporter](https://github.com/prometheus/node_exporter)**
- **[Solr Exporter](https://github.com/mosuka/solr-exporter)**

## Requirments
For **[MySQL Exporter](https://github.com/prometheus/mysqld_exporter)**, Create a user in mysql with these privileges
```sql
CREATE USER 'exporter'@'localhost' IDENTIFIED BY 'password';
GRANT PROCESS, REPLICATION CLIENT,
SELECT ON *.* TO 'exporter'@'localhost' WITH MAX_USER_CONNECTIONS 3;
FLUSH PRIVILEGES;
```
---
For **[Nginx Exporter](https://github.com/nginxinc/nginx-prometheus-exporter)**, We have to enable **stub_status** in nginx configuration. In your Nginx Conf add this line to your **location** block
```conf
location / {
    stub_status on;
}
```

## Role Variables
### Mandatory Variables
**Needs to be change depending upon environment**

|**Variables**| **Default Values**| **Description**|
|----------|---------|---------------|
|**prometheus_mysqld_exporter_env** |'user:password@(hostname:port)/'|User, password, host and port for mysql-exporter|
|**es_url** | localhost | Server IP of Elasticsearch|
|**es_port** | 9200 | Port on which elasticsearch is listening|
|**kafka_ip** | localhost | IP of the Kafka Server|
|**kafka_port** | 9092 | Port number on which kafka is running|
|**nginx_ip** | localhost | Server IP of nginx|
|**nginx_port** | 80 | Port number on which nginx is running|
|**solr_ip** | localhost | Server IP of the Solr server|
|**solr_port** | 8983 | Port number on which Solr is listening|

### Optional Variables

|**Variables**| **Default Values**| **Description**|
|--------------|-------------|-------------------|
|**node_exporter_version** | 0.17.0 | Version of Node Exporter|
|**solr_exporter_version** | 0.3.9 | Version of Solr Exporter|
|**apache_exporter** | 0.5.0 | Version of Apache Exporter|
|**es_exporter** | 1.0.2 | Version of Elasticsearch Exporter|
|**mongodb_exporter** | 1.0.0 | Version of MongoDB Exporter|
|**nginx_exporter** | 0.2.0 | Version of Nginx Exporter|
|**kafka_exporter_version** | 1.2.0 | Version of Kafka Exporter|
|**mysql_exporter_version** | 0.11.0 | Version of MySQL Exporter|

## Dependencies
None :-)

## Example Playbook
Here is an example playbook:-
```yml
---
- hosts: exporter
  user: ubuntu
  become: yes
  roles:
    - iamabhishek-dubey.ansible-role-prometheus-exporters
```

## Usage
For using this role you have to pass one variable to role which is **exporter_name**
```shell
ansible-playbook -i hosts site.yml -e exporter_name="node"
```
For running multiple exporter on same host you can use
```shell
ansible-playbook -i hosts site.yml -e exporter_name=["node", "apache"]
```

Values of **exporter_name** could be:-

|**Values** | **Description** |
|-----------|----------|
|**node** | For Node Exporter |
|**mysql** | For MySQL Exporter |
|**apache** | For Apache Exporter |
|**mongodb** | For MongoDB Exporter |
|**nginx** | For Nginx Exporter |
|**elasticsearch** | For Elasticsearch Exporter |
|**kafka** | For Kafka Exporter |
|**solr** | For Solr Exporter |

## Author
**[Abhishek Dubey](mailto:abhishek.dubey@opstree.com)**
