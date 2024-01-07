# Vagrantfile

Add this code to the Vagrantfile, below the `config.vm.box` line:

```ruby
config.vm.define "server1" do |server1|
  server1.vm.hostname = "server1"
end
config.vm.define "server2" do |server2|
  server2.vm.hostname = "server2"
end
```

# Create Two VMs

`vagrant up` - start **VM(s)** 

`vagrant ssh [name]` - connect to a **VM**
