# 运维

#### 安装go

wget https://dl.google.com/go/go1.11.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.11.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin

#### 安装restic

cd /opt
git clone https://github.com/restic/restic
cd restic
go run build.go
export PATH=$PATH:/opt/restic

备份：restic -r /srv/restic-repo backup --verbose ~/workdir
备份，显示详情：restic -r /srv/restic-repo backup --verbose --verbose ~/workdir
显示所有快照：restic -r /srv/restic-repo snapshots
从快照恢复：restic -r /srv/restic-repo restore latest --target /tmp/restore-work