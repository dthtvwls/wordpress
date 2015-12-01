Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 80, host: 80
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"

  config.vm.synced_folder ".", "/var/www/html/", owner: "www-data"

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    DEBIAN_FRONTEND=noninteractive apt-get install -y apache2 php5 php5-mysql mysql-server
    rm /var/www/html/index.html
    curl https://wordpress.org/latest.tar.gz | tar -xzC /var/www/html --strip-components=1
    cat << EOF | mysql -u root
        create database wordpress;
        create user 'username'@'localhost' identified by 'password';
        grant all privileges on wordpress.* to 'username'@'localhost';
EOF
  SHELL
end
