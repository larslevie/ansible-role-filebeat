# Ansible Role for Filebeat

Install and run Elastic Filebeat as a Docker container.

## Role Variables

```
filebeat_config:
  processors:
    - add_cloud_metadata: ~
  output.elasticsearch:
    hosts:
      - localhost
  filebeat.autodiscover:
    providers:
      - type: docker
        container.ids:
          - "*"
  filebeat.inputs:
    - type: docker
      containers.ids:
        - "*"
      processors:
        - add_docker_metadata: ~
filebeat_enabled: true
filebeat_image: docker.elastic.co/beats/filebeat-oss:6.4.0
filebeat_path: "/opt/filebeat"
filebeat_service: filebeat
```

## Dependencies

[lmickh.docker](https://galaxy.ansible.com/lmickh/docker)

## Example Playbook

```yaml
- name: servers
  hosts: "{{ target }}"
  gather_facts: yes
  roles:
    - "{{ larslevie.filebeat }}"
  vars:
    target: filebeat
```
