#Provision

## Provision GOCD

	ansible-playbook -i playbooks/hosts/gocd playbooks/gocd.yml

## Provision Elasticsearch

	ansible-playbook -i playbooks/hosts/es playbooks/es.yml

## Provision Kibana
The original source is from: https://github.com/azavea/ansible-kibana:

	ansible-playbook -i playbooks/hosts/kibana playbooks/kibana.yml

## Provision Logstash
See more detail about secure log aggregation, refer to: https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elk-stack-on-ubuntu-14-04

	ansible-playbook -i playbooks/hosts/logstash playbooks/logstash.yml
