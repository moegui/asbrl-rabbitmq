ASBRL-RABBITMQ
=========

Deploy a single RabbitMQ node as a Docker container.

Requirements
------------

Need to be Docker engine installed.

Role Variables
--------------

- default_user: 'ubuntu'
- HOSTNAME: ""
- DOCKER_LOG_DRIVER: "json-file"
- DOCKER_LOG_OPTIONS: "{}"
- IMAGE: "rabbitmq"
- BUILD: "3.8.7"
- USE_LONGNAME: "false"
- ERLANG_COOKIE: "supersecretcookie"
- PLUGINGS: rabbitmq_management
- VM_MEMORY_HIGH_WATERMARK: "0.61"
- DISCOVERY: "classic_config"
- DISCOVERY_AWS_PRIVATE_IP: "false"
- DISCOVERY_AWS_ASG: "true"
- DISCOVERY_AWS_TAG_NAME: "ClusterName"
- DISCOVERY_AWS_TAG_VALUE: ""
- CLEANUP_INTERVAL: 30
- CLEANUP_ONLY_LOG_WARNING: "false"
- PARTITION_HANDLING: "ignore"
- QUEUE_MASTER_LOCATOR: "min-masters"
- LOOPBACK_USERS: "none"
- LOG_LEVEL: "info"
- DOCKER_NETWORK_MODE: "bridge"
- CONTAINER_NAME: "rabbitmq"
- DOCKER_CPU_PERIOD: 0
- DOCKER_CPU_QUOTA: 0
- DOCKER_MEMORY: 0
- DOCKER_LABELS:
  - tag1: test
- ADMIN_USER: guest
- ADMIN_PASSWORD: guest

Dependencies
------------

None

Example Playbook
----------------

        - name: Deploy RabbitMQ Node
          include_role:
            name: asbrl-rabbitmq
          vars:
            DOCKER_LOG_DRIVER: "awslogs"
            DOCKER_LOG_OPTIONS: '{"awslogs-region":"{{REGION}}","awslogs-group":"{{LOGS_GROUP_NAME}}","tag":"{{ansible_nodename}}-rabbitmq"}'
            METRICS_INTERVAL: "{{PSCloudwatch.MetricsInterval}}"  
            RABBIT_PLUGINGS: rabbitmq_management,rabbitmq_peer_discovery_aws
            ERLANG_COOKIE: "{{PSRabbitMQ.ErlangCookie}}"
            VM_MEMORY_HIGH_WATERMARK: "{{PSRabbitMQ.VmMemoryHighWatermark}}"
            CLEANUP_INTERVAL: "{{PSRabbitMQ.NodeCleanupInterval}}"
            CLEANUP_ONLY_LOG_WARNING: "{{PSRabbitMQ.NodeCleanupOnlyWarning}}"
            PARTITION_HANDLING: "{{PSRabbitMQ.PartitionHandling}}"
            QUEUE_MASTER_LOCATOR: "{{PSRabbitMQ.QueueMasterLocator}}"
            LOOPBACK_USERS: "{{PSRabbitMQ.LoopbackUsers}}"
            LOG_LEVEL: "{{PSRabbitMQ.LogLevel}}"

License
-------

GNU General Public License v3.0 only

Author Information
------------------

Moegui.com