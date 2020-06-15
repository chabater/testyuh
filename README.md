# testyuh

    - name: copy file and archive
      unarchive:
        src: /ansible/playbook/source/kafka/kafka-manager-1.3.3.16.zip
        dest: /appool
        owner: kafka
        group: kafka

    - name: change kafka-manager name
      command: mv /appool/kafka-manager-1.3.3.16 /appool/kafka-manager

    - name: scp kafka-manager application.properties template
      template:
        src: /ansible/playbook/template/kafka/application.conf
        dest: /appool/kafka-manager/conf/application.conf

    - name: get kafka-manager application zk
      shell: grep ^kafka-manager.zkhosts=\'\" /appool/kafka-manager/conf/application.conf
      register: old_application_setting

    - name: show old_application_setting output
      debug:
        msg: "{{ old_application_setting.stdout }}"

    - name: new kafka-manager application zk
#      shell: echo {{ old_application_setting.stdout }} | sed 's/....$/\"/g' | sed 's/^kafka-manager.zkhosts=\'\\\"/^kafka-manager.zkhosts=\"/g'
      shell: echo {{ old_application_setting.stdout }} | sed 's/..$/\"/g'
      register: new_application_setting

    - name: show new_application_setting
      debug:
        msg: "{{ new_application_setting.stdout }}"

    - name: fix kafka-manager application zk
      lineinfile:
         state: present
         dest: /appool/kafka-manager/conf/application.conf
         regexp: '{{ old_application_setting.stdout }}'
         line: '{{ new_application_setting.stdout }}'
