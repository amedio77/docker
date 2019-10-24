# Docker 실습 (Centos 7)



## Docker  install

```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2

sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install -y docker-ce-3:18.09.9-3.*

sudo systemctl start docker && sudo systemctl enable docker

#centos user 에게 docker 실행 권한 부여 
sudo groupadd docker
sudo gpasswd -a ${USER} docker
sudo usermod -a -G docker $USER

exit

docker version
```



## Java  install

```
yum install java-1.8.0-openjdk-devel.x86_64
```



## Spring Music Sample Application Download 

- source download & compile

```java
git clone https://github.com/cloudfoundry-samples/spring-music
cd spring-music/
./gradlew clean assemble
```

- Dockerfile

```java
FROM openjdk:8-jdk-alpine
RUN mkdir /apps
COPY ./spring-music-1.0.jar /app/
WORKDIR /app
EXPOSE 8080
CMD ["java","-jar","/app/spring-music-1.0.jar"]
```

- Docker Image Build

```java
docker image build -t exam/hello:latest .
  
docker images
REPOSITORY                      TAG                 IMAGE ID            CREATED             SIZE
exam/hello                      latest              178ee4ff4918        40 minutes ago      161MB
```

- Docker run

```java
docker run --rm -p 8080:8080 -d exam/hello:latest
  
docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                        NAMES
c1edfd631a01        exam/hello:latest   "java -jar /app/spri…"   2 minutes ago       Up About a minute   0.0.0.0:8080->8080/tcp                       laughing_fermat
```



- localhost:8080 접속확인



## Spring PetClinic Sample Application  Download 

- source download & compile

```java
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic
./mvnw package
java -jar target/*.jar
```




