# testyuh

    - name: set kafka JAVA_HOME env
      lineinfile:
        state: present
        dest: /home/kafka/.bash_profile
        regexp: '^export JAVA_HOME'
        line: 'export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk'
        backup: yes

    - name: set kafka JRE_HOME env
      lineinfile:
        state: present
        dest: /home/kafka/.bash_profile
        regexp: '^export JRE_HOME'
        line: 'export JRE_HOME=/usr/lib/jvm/jre'
        backup: yes

    - name: set kafka ZOOKEEPER_HOME env
      lineinfile:
        state: present
        dest: /home/kafka/.bash_profile
        regexp: '^export ZOOKEEPER_HOME'
        line: 'export ZOOKEEPER_HOME=/appool/zookeeper/bin'
        backup: yes
