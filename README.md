# sonar

```
yum install java-1.8.0-openjdk-devel -y
alternatives --config javac
```
Download and Install SonarQube
```
yum install -y wget unzip
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.6.zip
unzip sonaquab
		or
sudo wget -O /etc/yum.repos.d/sonar.repo http://downloads.sourceforge.net/project/sonar-pkg/rpm/sonar.repo
sudo yum install sonar

chmod 777 /opt/ -R

vi /opt/sonarqube-7.6/conf/sonar.properties
add database username and password

cd /opt/sonar/bin/linux-x86-64/
vi sonar.sh
runas=user ec2-user

To start sonaquab
cd /opt/sonar/bin/linux-x86-64/
sh sonar.sh start
sh sonar.sh status

To check logs of sonal
cat /opt/sonarqube-7.6/logs/sonar.log


UI
http//:ouripaddress:9000

In sonar ui
admin
admin
account myaccount security
token
generate

jenkins:
configure system

 sonarquabe server
 name
 server url
 token
 ```
----------------------------------------------------------------------------------------
```
yum install -y @postgresql
postgresql-setup --initdb
systemctl start postgresql
systemctl enable postgresql
systemctl status postgresql
vi /var/lib/pgsql/data/postgresql.conf
systemctl restart postgresql
su - postgres
psql

CREATE DATABASE sonar;

CREATE USER sonar WITH PASSWORD 'StrongPassword';

ALTER USER sonar WITH PASSWORD 'StrongPassword';

GRANT ALL PRIVILEGES ON DATABASE sonar to StrongPassword;

------------------------

su - postgres
createuser sonar
CREATE DATABASE sonar OWNER sonar;
ALTER USER sonar WITH ENCRYPTED password 'StrongPassword';
```
--------------------------------------------------------------------------------------------
```
apache-maven
          conf-> vi settings.xml
                            plugingroup copy it plugin
                            <pluginGroup>org.sonarsource.scanner.maven</pluginGroup> 
                            in profile tag add plugins

<settings>
    <pluginGroups>
        <pluginGroup>org.sonarsource.scanner.maven</pluginGroup>
    </pluginGroups>
    <profiles>
        <profile>
            <id>sonar</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <properties>
                <!-- Optional URL to server. Default value is http://localhost:9000 -->
                <sonar.host.url>
                  http://54.224.87.69:9000
                </sonar.host.url>
            </properties>
        </profile>
     </profiles>
</settings>
```
-----------------------------------------------------
```
sonarquabescanner


analyzing with sonarqube scanner
sonar scanner cli plugin
cd/opt/ sonar-scanner-3..............
vi sonar.scanner.properties
sonar.host.url=http.....



sonar.hosst.url=ip
sonar.projectName=mavenwebappdemo
sonar.projectkey=mavenwebappsdemo
sonar.projectversion=1.0
sonar.sources=mavenwebappdemo
```

-----------------------------------------------------------------------

```
docker run -d --name sonarqube -p 9000:9000 sonarqube

		or

docker run -d --name sonarqube \
    -p 9000:9000 \
    -e sonar.jdbc.username=sonar \
    -e sonar.jdbc.password=sonar \
    -e sonar.jdbc.url=jdbc:postgresql://localhost/sonar \
    sonarqube
```

https://www.baeldung.com/sonar-qube
https://blog.knoldus.com/integrate-maven-project-sonarqube/
https://dzone.com/articles/sonarcloud-integration-with-springboot-maven
