# testyuh

    - name: mode check again
      command: chown -R kafka.kafka /appool/zookeeper /appool/kafka /appool/kafka-manager

    - name: stop firewalld
      service:
        name: firewalld
        state: stopped
        enabled: no

    - name: restart zookeeper servivce
      systemd: name=zookeeper state=started enabled=yes

    - name: restart kafka servivce
      systemd: name=kafka state=started enabled=yes

    - name: restart kafka-manager servivce
      systemd: name=kafka-manager state=started enabled=yes

    - name: restart zookeeper servivce
      service:
        name: zookeeper.service
        state: restarted

    - name: restart kafka servivce
      service:
        name: kafka.service
        state: restarted

    - name: restart kafka-manager servivce
      service:
        name: kafka-manager.service
        state: restarted

    - name: restart zookeeper servivce
      command: systemctl restart zookeeper.service

    - name: restart kafka servivce
      command: systemctl restart kafka.service

    - name: restart kafka-manager servivce
      command: systemctl restart kafka-manager.service
