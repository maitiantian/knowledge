<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a href="javascript:void(0)" style="color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# 目录

* [使用restic备份](#使用restic备份)


# <p align="center" style="border-bottom: 3px solid #e7e7e7;">使用restic备份</p>


#### 安装go

```bash
wget https://dl.google.com/go/go1.11.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.11.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
```

#### 安装restic

```bash
cd /opt
git clone https://github.com/restic/restic
cd restic
go run build.go
export PATH=$PATH:/opt/restic
```

* 备份：restic -r /srv/restic-repo backup --verbose ~/workdir
* 备份，显示详情：restic -r /srv/restic-repo backup --verbose --verbose ~/workdir
* 显示所有快照：restic -r /srv/restic-repo snapshots
* 从快照恢复：restic -r /srv/restic-repo restore latest --target /tmp/restore-work