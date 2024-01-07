# Create VM and Provision using script
Now we will focus on creating multiple VMs and executing a script automatically when we run `vagrant up`.

## The script
Create a "script.sh" file, then put the commands to install Nginx:
```bash 
#! /bin/bash
sudo apt update
sudo apt install -y nginx
```

## Vagrantfile

Add this code to the Vagrantfile, below the `config.vm.box` line:

```ruby
config.vm.provision "shell", path: "script.sh"
config.vm.define "server1" do |server1|
  server1.vm.hostname = "server1"
end
config.vm.define "server2" do |server2|
  server2.vm.hostname = "server2"
end
```

## Create Two VMs

`vagrant up` - start **VM(s)** 

`vagrant ssh [name]` - connect to a **VM**

When you want to return to the host simply use the `exit` command in the terminal of the VM you are connected to.

## Check Nginx status
To check Nginx status use the following command when connected to the VM, use the following command:
```bash
sudo systemctl status nginx
```

If the output is similar to the following:
```bash
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2024-01-07 15:03:14 EST; 1min 33s ago
       Docs: man:nginx(8)
    Process: 2488 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, statu>
    Process: 2489 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCE>
   Main PID: 2573 (nginx)
      Tasks: 3 (limit: 2191)
     Memory: 4.6M
        CPU: 25ms
     CGroup: /system.slice/nginx.service
             ├─2573 "nginx: master process /usr/sbin/nginx -g daemon on; master_process on;"
             ├─2576 "nginx: worker process" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" ">
             └─2577 "nginx: worker process" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" "" ">

Jan 07 15:03:14 server2 systemd[1]: Starting A high performance web server and a reverse proxy server...
Jan 07 15:03:14 server2 systemd[1]: Started A high performance web server and a reverse proxy server.
```
That means Nginx is active and has successfully installed.

## Destroy VMs

To destroy the VMs, return to the host terminal (after exiting from the VM) use the following command:
```bash
vagrant destroy
```
