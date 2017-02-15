Role for adding new clients to prometheus monitoring.

Role added new config with client's name to ```/etc/prometheus/file_sd_configs``` and edit /etc/hosts

Requirements
------------

1) group ```monitoring``` with hosts called by names and with vars ```int_it```(internal ip) and ``` exporter_ports ``` should be  in ```inventory```
```
[monitoring]
test ansible_host=<host_external_ip> int_ip=<host_internal_ip> exporter_ports='["<node_exporter_port>", "<other_exporter_port>"]'
```

2) Smth like this  should be in ```/etc/prometheus/prometheus.yml```
```
        file_sd_configs:
            - files:
                - '/etc/prometheus/file_sd_configs/*.yml'
```

### Example of execution ```example/monitoring-client.yml```

```
ansible-playbook monitoring-client.yml -e client=test
```

without editting /etc/hosts

```
ansible-playbook monitoring-client.yml -e client=test --skip-tags hosts
```

------------

Роль для добавления новых клиентов в мониторинг.

Роль кладет в директорию ```/etc/prometheus/file_sd_configs``` новый конфиг по имени клиента

Requirements
------------
1) В ```inventory``` должна быть выделенная группа ```monitoring```, в которой будут указаны хосты по именам, у которых будут выписана переменная```int_it```(внутренний адрес), а также выписаны порты для экспортеров ``` exporter_ports ``` или же указаны в host_vars файле.
```
[monitoring]
test ansible_host=<host_external_ip> int_ip=<host_internal_ip> exporter_ports='["<node_exporter_port>", "<other_exporter_port>"]'
```

2) В конфиге ```/etc/prometheus/prometheus.yml``` должно быть указано
```
        file_sd_configs:
            - files:
                - '/etc/prometheus/file_sd_configs/*.yml'
```

### Пример запуска ```example/monitoring-client.yml``` плейбука для использования роли

```
ansible-playbook monitoring-client.yml -e client=test
```

для запуска без редактирования /etc/hosts

```
ansible-playbook monitoring-client.yml -e client=test --skip-tags hosts
```