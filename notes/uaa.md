# UAA

```
# Basic package updates
sudo apt-get update
sudo apt-get install build-essential

# Ruby
sudo apt-get install ruby
sudo apt-get install ruby-dev

# UAA command line tool
sudo gem install cf-uaac

# Java
sudo apt-get install openjdk-11-jdk

# Custom uaa.yml location with overrides
export CLOUDFOUNDRY_CONFIG_PATH=/mnt/c/Users/Ry/cybr406-2020/projects

# Certificates for JWT signing
mkdir uaa-certs
cd uaa-certs
openssl genrsa -out privkey.pem 2048
openssl rsa -pubout -in privkey.pem -out pubkey.pem

# Export keys for UAA t pick up
export JWT_TOKEN_SIGNING_KEY=$(cat privkey.pem)
export JWT_TOKEN_VERIFICATION_KEY=$(cat pubkey.pem)
```
