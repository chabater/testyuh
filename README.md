# testyuh

[Unit]
Description=Zookeeper
Requires=network.target remote-fs.target
After=network.target remote-fs.target

[Service]
Type=forking
User=kafka
Group=kafka
ExecStart=/appool/zookeeper/bin/zkServer.sh start
ExecStop=/appool/zookeeper/bin/zkServer.sh stop
ExecReload=/appool/zookeeper/bin/zkServer.sh restart
WorkingDirectory=/appool/zookeeper

[Install]
WantedBy=multi-user.target
