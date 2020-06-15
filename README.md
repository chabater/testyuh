# testyuh



    - name: check lv exist
      command: "grep appool /etc/fstab"
      register: fstab_appool_exist
      ignore_errors: yes

    - name: check lv full name
      shell: "lsblk -fp | grep appool | awk '{print $1}' | sed 's/^..//g'"
      register: appool_full_name
      ignore_errors: yes

    - name: check lv filesystem type
      shell: "lsblk -fp | grep appool | awk '{print $2}'"
      register: appool_filesystem_type
      ignore_errors: yes

    - name: change fstab appool line
      lineinfile:
        state: present
        dest: /etc/fstab
        regexp: '^{{appool_full_name.stdout}}'
        line: '{{appool_full_name.stdout}} /appool {{appool_filesystem_type.stdout}} defaults,noatime 1 2'
        backup: yes
      when: fstab_appool_exist != 0

    - name: add sysctl parameter
      blockinfile:
        path: /etc/sysctl.conf
        block: |
          vm.swappiness=1
          vm.dirty_background_ratio=5
          vm.dirty_ratio=60
          net.ipv4.tcp_tw_recycle=1
        backup: yes

    - name: copy kafka.conf limit file
      copy:
        src: /ansible/playbook/template/kafka/kafka.conf
        dest: /etc/security/limits.d/kafka.conf
        owner: kafka
        group: kafka

    - name: copy kafka.conf limit file
      copy:
        dest: /etc/security/limits.d/kafka.conf
        content: 'kafka        -     nofile   655350'
