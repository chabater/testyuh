# testyuh

kafka-manager.zkhosts='"{% for host in groups['new_kafka_cluster'] %}{{ hostvars[host].ansible_default_ipv4.address }}:2181,{% endfor %}"'
