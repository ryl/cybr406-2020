# UAA

## Install Setup

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
```

## UAA Configuration

```
# Certificates for JWT signing
mkdir uaa-certs
cd uaa-certs
openssl genrsa -out privkey.pem 2048
openssl rsa -pubout -in privkey.pem -out pubkey.pem
```

The contents of the keys can be added directly to uaa.yml using the yml
multiline format.

## Running from Gradle

```
# Use a database
export SPRING_PROFILES=postgresql,default

# Custom uaa.yml location with overrides
export CLOUDFOUNDRY_CONFIG_PATH=/mnt/c/Users/Ry/cybr406-2020/projects

# Export keys for UAA to pick up
export JWT_TOKEN_SIGNING_KEY=$(cat privkey.pem)
export JWT_TOKEN_VERIFICATION_KEY=$(cat pubkey.pem)
```

## Tomcat Configuration

```
# UAAC needs a SSL certificate
keytool -genkey -keyalg RSA -alias uaa -keystore keystore.jks -storepass password -validity 360 -keysize 2048
```

server.xml

```
<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
           maxThreads="150" SSLEnabled="true">
    <SSLHostConfig>
        <Certificate certificateKeystoreFile="conf/keystore.jks"
                     certificateKeystorePassword="password"
                     type="RSA" />
    </SSLHostConfig>
</Connector>
```

tomcat-users.xml

```
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="manager" password="manager" roles="manager-gui,manager-script,admin-gui"/>
```

Increase max upload size for manager in `webapps/manager/WEB-INF/web.xml`

```
<multipart-config>
  <!-- 100MB max -->
  <max-file-size>104857600</max-file-size>
  <max-request-size>104857600</max-request-size>
  <file-size-threshold>0</file-size-threshold>
</multipart-config>
```

## Running From Tomcat as a WAR

Build the WAR file.

```
./gradlew :cloudfoundry-identity-uaa:war
```

Set CATALINA_OPTS before starting Tomcat.

```
# Launch tomcat with uaa settings configured
export CATALINA_OPTS="-DCLOUDFOUNDRY_CONFIG_PATH=/mnt/c/Users/Ry/cybr406-2020/projects/uaa-conf -Dlogging.config=/mnt/c/Users/Ry/cybr406-2020/projects/uaa-conf/log4j2.properties"
```

# UAAC

* <https://docs.cloudfoundry.org/concepts/architecture/uaa.html>
* <https://www.baeldung.com/cloud-foundry-uaa>

```
uaac target http://localhost:8080/uaa
uaac token client get admin -s adminsecret

# Create a client
uaac client add webappclient -s webappclientsecret --name WebAppClient --scope "resource.read,resource.write,openid,pro
file,email,address,phone" --authorized_grant_types "authorization_code,refresh_token,client_credentials,password" --authorities uaa.resource --redirect_uri http://localhost:8081/login/oauth2/code/uaa

# Create a user
uaac user add lowryrs -p secret --emails lowryrs@unk.edu
```
