# testyuh

[Unit]
Requires=zookeeper.service
After=zookeeper.service

[Service]
Type=simple
User=kafka
ExecStart=/bin/sh -c '/appool/kafka/bin/kafka-server-start.sh /appool/kafka/config/server.properties > /var/log/kafka.log 2>&1'
ExecStop=/appool/kafka/bin/kafka-server-stop.sh
Restart=on-abnormal

[Install]
WantedBy=multi-user.target

