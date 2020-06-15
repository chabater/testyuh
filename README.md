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



# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just
# example sakes.
dataDir=/appool/zookeeper
# the port at which the clients will connect
clientPort=2181
# the maximum number of client connections.
# increase this if you need to handle more clients
#maxClientCnxns=60
#
# Be sure to read the maintenance section of the
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1
server.1=:2888:3888
server.2=:2888:3888
server.3=:2888:3888

## Metrics Providers
#
# https://prometheus.io Metrics Exporter
metricsProvider.className=org.apache.zookeeper.metrics.prometheus.PrometheusMetricsProvider
metricsProvider.httpPort=7000
metricsProvider.exportJvmInfo=true
