vector-role
=========

Роль vector-role устанавливает vector на подготовленную инфраструктуру, конфигурируется с помощь шаблона

Role Variables
--------------

Переменные в defaults/main.yml:
vector_version: "0.30.0"
vector_path: "/opt/vector/"
vector_data_dir: "/var/lib/vector/"

Конфигруация Vector задается через переменные defaults
/main.yml, например:

      vectorconfig:
        sources:
          stdin_source:
            type: stdin
        transforms:
          transform_stdin:
            type: remap
            inputs:
              - stdin_source
        sinks:
          my_sink_id:
            type: clickhouse
            inputs:
              - transform_stdin
            compression: gzip
            database: logs
            endpoint: http://{{ clickhouse }}:8123
            table: logstable

Шаблон конфигурации Vector templates/vector_config.j2

License
-------

BSD

