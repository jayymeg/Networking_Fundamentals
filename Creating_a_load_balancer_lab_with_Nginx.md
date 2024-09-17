```markdown
# Creating a Load Balancer Lab with Nginx and Multiple Vagrant Servers

## Objective
Create a load balancer lab using Nginx, three web servers, and one Nginx server. The web servers should host informative HTML webpages.

## Prerequisites
- Install VirtualBox: Download and install VirtualBox from [VirtualBox's official website](https://www.virtualbox.org/).
- Install Vagrant: Download and install Vagrant from the [Vagrant website](https://www.vagrantup.com/).

## Step 1: Prepare the Lab Directory
Create a new directory for your project and navigate to it in your terminal. This directory will contain the Vagrant configuration files.

```bash
mkdir load_balancer_lab
cd load_balancer_lab
```
![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%201-2.png)

## Step 2: Set Up Vagrant Configuration
Create a `Vagrantfile` to define your virtual machines and their configurations.

```ruby
Vagrant.configure("2") do |config|
  config.vm.define "nginx" do |nginx|
    nginx.vm.box = "ubuntu/bionic64"
    nginx.vm.network "private_network", type: "dhcp"
    nginx.vm.provision "shell", path: "provision/nginx.sh"
  end

  # Configuration for Web Server 1
  config.vm.define "web1" do |web1|
    web1.vm.box = "ubuntu/bionic64"
    web1.vm.network "private_network", type: "dhcp"
    web1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y nginx
      echo "This is Web Server 1" > /var/www/html/index.html
    SHELL
  end

  # Configuration for Web Server 2
  config.vm.define "web2" do |web2|
    web2.vm.box = "ubuntu/bionic64"
    web2.vm.network "private_network", type: "dhcp"
    web2.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y nginx
      echo "This is Web Server 2" > /var/www/html/index.html
    SHELL
  end

  # Configuration for Web Server 3
  config.vm.define "web3" do |web3|
    web3.vm.box = "ubuntu/bionic64"
    web3.vm.network "private_network", type: "dhcp"
    web3.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y nginx
      echo "This is Web Server 3" > /var/www/html/index.html
    SHELL
  end
end
```
![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%202.png)

## Step 3: Create Provisioning Scripts
Create provisioning scripts for Nginx and the web servers.

![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%203.png)

### Create `provision/nginx.sh`:

```bash
#!/bin/bash
apt-get update
apt-get install -y nginx
```
![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%203(1).png)

### Create `provision/webserver.sh`:

```bash
#!/bin/bash
apt-get update
apt-get install -y nginx

# Check the hostname and set content accordingly
if [[ $(hostname) == "web1" ]]; then
    echo "This is Web Server 1" > /var/www/html/index.html
elif [[ $(hostname) == "web2" ]]; then
    echo "This is Web Server 2" > /var/www/html/index.html
elif [[ $(hostname) == "web3" ]]; then
    echo "This is Web Server 3" > /var/www/html/index.html
else
    echo "This is a default page" > /var/www/html/index.html
fi
```
![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%203(2).png)

## Step 4: Initialize and Start Vagrant Machines
Navigate to your project directory and run the following command:

```bash
vagrant up
```

This will initialize and start the Nginx and web server virtual machines based on your Vagrant configuration.
![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%204.png)

![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%204.png)

## Step 5: Configure Nginx Load Balancer
SSH into the Nginx virtual machine:

```bash
vagrant ssh nginx
```
![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%205.png)

Edit the Nginx configuration file to set up load balancing:

```bash
sudo nano /etc/nginx/sites-available/default
```
![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%205(2).png)

Edit the file to include the following configuration inside the server block:

```nginx
location / {
    proxy_pass http://web_servers;
}

upstream web_servers {
    server <web1_ip>:80;
    server <web2_ip>:80;
    server <web3_ip>:80;
}
```

Replace `<web1_ip>`, `<web2_ip>`, and `<web3_ip>` with the actual private IPs of your web server VMs.

![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%205(1).png)


## Step 6: Test the Load Balancer
Open a web browser on your local machine and navigate to the private IP address of your Nginx VM. You should see the load-balanced web servers serving informative HTML pages in a round-robin manner.

## Step 7: Verify Load Balancing
To verify that load balancing is working, SSH into each web server and check their access logs:

![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%207.png)

```bash
vagrant ssh web1
tail -f /var/log/nginx/access.log

vagrant ssh web2
tail -f /var/log/nginx/access.log

vagrant ssh web3
tail -f /var/log/nginx/access.log
```

You should see that requests are being distributed between the three web servers, demonstrating successful load balancing.

## Step 8: Check Load Balancing in a Web Browser
On your local machine (not within the virtual machines), open a web browser. In the browser's address bar, type the private IP address of your Nginx virtual machine. Press Enter. You should observe the load-balanced web servers in action, confirming that Nginx is successfully load-balancing the requests.
```

![my image](https://github.com/jayymeg/Networking_Fundamentals/blob/master/load%20balancer%20lab/step%208.png)
