# testyuh

    - name: Modify kafka start shell
      lineinfile:
         state: present
         dest: /appool/kafka/bin/kafka-server-start.sh
         regexp: 'export KAFKA_HEAP_OPTS="-Xmx1G -Xms1G"'
         line: 'export KAFKA_HEAP_OPTS="-Xmx4G -Xms4G -XX:MetaspaceSize=96m -XX:+UseG1GC -XX:MaxGCPauseMillis=20 -XX:InitiatingHeapOccupancyPercent=35 -XX:G1HeapRegionSize=16M -XX:MinMetaspaceFreeRatio=50 -XX:MaxMetaspaceFreeRatio=80"'

    - name: Modify kafka start shell
      lineinfile:
         state: present
         dest: /appool/kafka/bin/kafka-server-start.sh
         insertafter: '^export KAFKA_HEAP_OPTS="-Xmx4G -Xms4G'
         line: 'export JMX_PORT="9999"'
