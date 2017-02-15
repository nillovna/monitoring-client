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