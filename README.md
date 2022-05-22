# apache-tomcat

It is made out of 3 parts:

1. Catalina - handles the interface between servlets and the rest of tomcat, handles urls routing to different servlets
2. Jasper - is the component that compiles jsp files into servlets
3. Coyote - handles the http and lets it act like a server

## Linux installation

Install Java

Add JAVA_HOME environment variable to /etc/environment

```
JAVA_HOME="/usr/lib/jvm/default-java"
```

Create tomcat user

```
sudo useradd -m -d /opt/tomcat -U -s /bin/false tomcat
```

Download tomcat 8

```
wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.78/src/apache-tomcat-8.5.78-src.tar.gz
```

Extract and copy to home

```
sudo tar xzvf apache-tomcat-8*tar.gz -C /app/tomcat --strip-components=1
```


Edit this file

/opt/tomcat/webapps/manager/META-INF/context.xml


Update/Create the tomcat users

```
sudo cp tomcat-users.xml /opt/tomcat/conf/tomcat-users.xml
```

Create the tomcat service

```
sudo cp tomcat.service /etc/systemd/system/tomcat.service
```

Start tomcat service


```
sudo systemctl start tomcat.service
```


Enable tomcat service


```
sudo systemctl enable tomcat.service
```

Check the tomcat service status


```
sudo systemctl status tomcat.service
```

Enter this command to fix error: Failed to connect to bus: Host is down

```
sudo nsenter -t $(pidof systemd) -m -p su - $LOGNAME
```

### Systemd

Daemon = system service

"services that run in the background"

Linux services naming convention (ends with 'd')

- httpd
- smbd
- sshd
- dhcpd

In some systems services were started one at a time using **/etc/init.d**, which would be the first process to run

Command used to manage system units: [systemctl](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_basic_system_settings/managing-system-services-with-systemctl_configuring-basic-system-settings)

```
systemctl
```


## MAC installation 

Check Java is installed

Check Java version is compatible with tomcat using the [docs](https://tomcat.apache.org/whichversion.html)

```
java -version
```

Set Java environ variable 

```
export JAVA_HOME=$(/usr/libexec/java_home)
```

Download the tomcat binary (tar.gz) and save to the downloads folder

Move the files

```
sudo mkdir -p /usr/local
```

```
sudo mv ~/Downloads/apache-tomcat-8.5.78 /usr/local
```

Create a symbolic link

```
sudo rm -f /Library/Tomcat
```

```
sudo ln -s /usr/local/apache-tomcat-8.5.78 /Library/Tomcat
```

Change the folder ownership

```
sudo chown -R <your_username> /Library/Tomcat
```

Make scripts in folder executable

```
sudo chmod +x /Library/Tomcat/bin/*.sh
```

Start and stop service

```
/Library/Tomcat/bin/startup.sh
```

```
/Library/Tomcat/bin/shutdown.sh
```

## Creating a webapp

copy the .war file in the webapps folder

e.g
```
cp /Downloads/helloworld.war /Library/Tomcat/webapps/
```

By default tomcat is on port 8080

Therefore you can access the helloworld app on http://[your-server]:8080/helloworld

