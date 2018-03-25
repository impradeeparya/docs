# Docker commands

1. **Show images**

    ```
        pradeep@xe-tlindual-parya:~$ sudo docker images
        REPOSITORY                         TAG                 IMAGE ID            CREATED             SIZE
        tomcat                             8-jre8              bcf14fe73b2b        3 days ago          333 MB
        ubuntu                             14.04               b969ab9f929b        3 weeks ago         188 MB
        pradeep@xe-tlindual-parya:~$
    ```

2. **Show containers**
    - **show running containers**
    ```
       pradeep@xe-tlindual-parya:~$ sudo docker ps
       CONTAINER ID        IMAGE               COMMAND             CREATED                  STATUS                      PORTS                                   NAMES
       e003edcf1ae9        tomcat              "catalina.sh run"   19 seconds ago       Up 19 seconds          0.0.0.0:8080->8080/tcp     tomcat
       pradeep@xe-tlindual-parya:~$
    ```
    - **show all containers**
    ```
        pradeep@xe-tlindual-parya:~$ sudo docker ps -a
        CONTAINER ID        IMAGE           COMMAND                 CREATED                STATUS                               PORTS                                   NAMES
        e003edcf1ae9        tomcat          "catalina.sh run"       2 minutes ago        Up 2 minutes                     0.0.0.0:8080->8080/tcp     tomcat
        dac80295dc8e       tomcat           "catalina.sh run"      2 days ago              Exited (130) 2 days ago                                                  datetime-app
        pradeep@xe-tlindual-parya:~$
    ```
    - **show only container ids**
    ```
    pradeep@xe-tlindual-parya:~$ sudo docker ps -a -q
    e003edcf1ae9
    6c120e16d55b
    dac80295dc8e
    ```
3. **Remove image**
    ```
    docker rmi -f <IMAGE_ID>
    ```
4. **Remove container**
    ```
    docker rm <CONTAINER_ID>
    ```
5. **Create docker file**

    ```
    # Pull base image
    FROM ubuntu:14.04
    # Install java-8
        RUN \
         echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
         apt-get update && \
         apt-get install -y software-properties-common && \
         add-apt-repository -y ppa:webupd8team/java && \
         apt-get update && \
         apt-get install -y oracle-java8-installer && \
         rm -rf /var/lib/apt/lists/* && \
         rm -rf /var/cache/oracle-jdk8-installer

    # Define commonly used JAVA_HOME variable
    ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
    ```

    > save above commands in a file name **Dockerfile**(without any extension), it will create a docker image with ubuntu as base image and java8 is installed on it after building **Dockerfile**.

6. **Build image**
    ```
    docker build -t <IMAGE_NAME> .
    ```

    > above command will search for **Dockerfile** in current folder to build image.

7. **Run container**
    ```
    docker run <IMAGE_ID>
    ```

8. **Open container terminal**
    ```
    docker run -it -d <IMAGE_ID>
    ```
    > above command will run container in detached mode with valid tty attached to it.
    docker run -p 8080:8080 -d 7e949acc4b99

    ```
    docker attach <CONTAIER_ID>
    ```
    > above command will open attached tty to given container.
9. **Deploy war**
    - **Expose war directory path to server deployment directory**
    ```
    ADD <WAR_PATH> <TOMCAT_WEBAPP_PATH>
    ```
    > add above command in **Dockerfile**

    ```
    sudo docker run -it --rm -p 8080:8080 --name <WAR_NAME> <IMAGE_NAME>:<VERSION>
    ```
    > above command to deploy war in 8080 port

10. **Option in command**
    - it   : interactive
    - rm   : rm container after exit
    - p    : port
    - name : name of container

11. **Tag image with repository name of docker hub**
    ```
    docker tag <IMAGE_ID> <DOCKER_HUB_USERNAME>/<IMAGE_NAME>:<VERSION>
    ```
12. **Push image**
    ```
    docker push <REPOSITORY_NAME>:<VERSION>
    ```
