# 修改Ubuntu16.04 swap分区的大小

### 创建一个swap文件：
```shell
$ sudo dd if=/dev/zero of=/swapfile bs=1M count=16k    # swapfile == 16GB
```

### 格式化新增的swap文件
```shell
sudo mkswap /swapfile
```

### 锁定文件的权限
我们需要锁定文件的权限，以便只有拥有root权限的用户才能读取文件内容，这可以防止普通用户能够访问该文件，以免造成重大的安全隐患。
```shell
sudo chmod 600 /swapfile
```

### 启动新增的swap文件
```shell
sudo swapon /swapfile
```

运行上面命令后，再次通过`free -h`命令就可以看到，swap分区增大了16G。


### 开机后自动启动新增的swap文件
我们最近的更改启用了当前会话的swap文件，但是，如果我们重新启动，服务器不会自动保留swap设置
我们可以通过将swap文件添加到`/etc/fstab`文件中来改变这一点:
在`/etc/fstab文件最后增加`：`/swapfile swap swap defaults 0 0`

```shell
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

