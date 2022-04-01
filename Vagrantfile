$script = <<-'SCRIPT'
#Instala Node
  apt update
  apt install -y curl 
  apt install -y gnupg2 
  apt install -y wget 
  apt install -y npm
  apt install -y gpg
  curl -sL https://deb.nodesource.com/setup_16.x | sudo bash -
  apt -y install nodejs
  apt update
  node  -v
#Instala Mongo
  cd /tmp
  echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/5.0 main" | tee /etc/apt/sources.list.d/mongodb-org-5.0.list
  curl -sSL https://www.mongodb.org/static/pgp/server-5.0.asc  -o mongoserver.asc
  gpg --no-default-keyring --keyring ./mongo_key_temp.gpg --import ./mongoserver.asc
  gpg --no-default-keyring --keyring ./mongo_key_temp.gpg --export > ./mongoserver_key.gpg
  mv mongoserver_key.gpg /etc/apt/trusted.gpg.d/
  apt update
  apt install -y mongodb-org 
  apt install -y  node-mongodb
  apt autoremove
  systemctl enable mongod
  systemctl start mongod
#Install Genieacs
  npm install -g genieacs
  useradd --system --no-create-home --user-group genieacs
  mkdir /opt/genieacs
  mkdir /opt/genieacs/ext
SCRIPT


Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"
  config.vm.provision "shell", inline: $script
  
end



