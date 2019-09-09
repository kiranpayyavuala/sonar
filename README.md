# sonar

```
sudo yum install -y java-11-openjdk-devel
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

vi /opt/sonarqube-7.6/conf/sonar.properties(add database username and password)
sonar.jdbc.username=sonar
sonar.jdbc.password=PASSWORD
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonardb

cd /opt/sonar/bin/linux-x86-64/
vi sonar.sh
runas=user ec2-user

To start sonaquab
cd /opt/sonar/bin/linux-x86-64/
sh sonar.sh start
sh sonar.sh status

To check logs of sonal
cat /opt/sonarqube-7.6/logs/sonar.log
cat /opt/sonarqube-7.6/logs/web.log
```
For Sonar UI
http//:ouripaddress:9000
```
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
#Install postgres
```
yum install -y @postgresql
postgresql-setup --initdb

vi /var/lib/pgsql/data/postgresql.conf
Listenaddress='*'

vi /var/lib/pgsql/data/pg_hba.conf(change to trust)
local	all	all	trust
host	all	0.0.0.0/0	trust

systemctl start postgresql
systemctl enable postgresql
systemctl status postgresql

su - postgres
psql

create sonar user and database

\q
exit
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
                  http://ip:9000
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
