# testyuh

[Unit]
Description=kafka manager service
Requires=network.target
After=network.target kafka.service

[Service]
ExecStart=/appool/kafka-manager/bin/kafka-manager -Dconfig.file=/appool/kafka-manager/conf/application.conf
ExecStop=/usr/local/kafka-manager/bin/kafka-manager stop
User=kafka
Type=simple

[Install]
WantedBy=multi-user.target

