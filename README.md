# testyuh

    - name: scp kafka server.properties template
      template:
        src: /ansible/playbook/template/kafka/server.properties
        dest: /appool/kafka/config/server.properties

    - name: get zookeeper.connect
      shell: grep ^zookeeper.connect= /appool/kafka/config/server.properties
      register: old_zookeeper_setting

    - name: new zookeeper.connect
      shell: echo {{ old_zookeeper_setting.stdout }} | sed 's/.$//g'
      register: new_zookeeper_setting

    - name: fix zookeeper setting
      lineinfile:
         state: present
         dest: /appool/kafka/config/server.properties
         regexp: '{{ old_zookeeper_setting.stdout }}'
         line: '{{ new_zookeeper_setting.stdout }}'

    - name: setting kafka server config listeners
      lineinfile:
         state: present
         dest: /appool/kafka/config/server.properties
         regexp: '^listeners=PLAINTEXT://TaRHKaf01:9092'
         line: 'listeners=PLAINTEXT://{{ ansible_default_ipv4.address }}:9092'

    - name: setting kafka server config advertised
      lineinfile:
         state: present
         dest: /appool/kafka/config/server.properties
         regexp: '^advertised.listeners=PLAINTEXT://TaRHKaf01:9092'
         line: 'advertised.listeners=PLAINTEXT://{{ ansible_default_ipv4.address }}:9092'

    - name: create kafka log
      file:
        path: /var/log/kafka.log
        owner: kafka
        group: kafka
        mode: 0755
        state: touch
