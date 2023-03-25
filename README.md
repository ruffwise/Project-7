# Project-7: Devops Tooling Website Solution

### create partition on NFS server

![partition](/images/partition.png)

### create physical disk

![](/images/physical_disk.png)

### add physical disk to volume group

`sudo vgcreate NFS-vg /dev/xvdf1 /dev/xvdg1 /dev/xvdh1`

![](/images/volume_group.png)

### create logical volume

'sudo lvcreate -n lv-apps -L 9G NFS-vg'

`sudo lvcreate -n lv-logs -L 9G NFS-vg`

`sudo lvcreate -n lv-opt -L 9G NFS-vg`
![](/images/logical_vol.png)

### format the disks

`sudo mkfs -t xfs /dev/NFS-vg/lv-apps`
`sudo mkfs -t xfs /dev/NFS-vg/lv-logs`
`sudo mkfs -t xfs /dev/NFS-vg/lv-opt`
![](/images/format-disk.png)

### mount directories on logical volume

`sudo mkdir /mnt/apps`
`sudo mkdir /mnt/logs`
`sudo mkdir /mnt/opt`
![](/images/mount.png)

### update /ETC/Fstab file

### install NFS

`sudo yum -y update`

`sudo yum install nfs-utils -y`

`sudo systemctl start nfs-server.service`

`sudo systemctl enable nfs-server.service`

`sudo systemctl status nfs-server.service`
![](/images/NFS-service.png)

### setup permissions on mount directory

![](/images/permission.png)

### configure access to NFS for clients within the same subnet

![](/images/NFS-access.png)

### configure database server

![](/images/sql-user.png)

### install NFS client

`sudo yum install nfs-utils nfs4-acl-tools -y`

### mount /var/www/ on NFS server

![](/images/var-www-mount.png)

### install remi's repository, apache and PHP

`sudo yum install httpd -y`

`sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`

`sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`

`sudo dnf module reset php`

`sudo dnf module enable php:remi-7.4`

### mount log folder on NFS server

`sudo mount -t nfs -o rw,nosuid 172.31.40.44:/mnt/logs/web1 /var/log/httpd`

`sudo mount -t nfs -o rw,nosuid 172.31.40.44:/mnt/logs/web2 /var/log/httpd`

![](/images/login_page.png)
![](/images/webpage.png)
