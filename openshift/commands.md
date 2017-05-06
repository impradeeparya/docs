# Openshift Commands

1. **Login**
    ```
    oc login <TOKEN>
    ```
2. **Show projects**
    ```
    oc projects
    ```
3. **Select project**
    ```
    oc project <PROJECT_NAME>
    ```
4. **Show status of projects**
    ```
    oc status
    ```
5. **Create new application on openshift**

    - **Create new application with source code in git**
    ```
    oc new-app <GIT_CLONE_URL>
    ```

        **Example**
        ```
        oc new-app https://github.com/impradeeparya/datetime-app.git


        error: multiple images or templates matched "jee": 5

        The argument "jee" could apply to the following Docker images, OpenShift image streams, or templates:

        * Image stream "wildfly" (tag "10.0") in project "openshift"
          Use --image-stream="openshift/wildfly:10.0" to specify this image or template

        * Image stream "wildfly" (tag "10.1") in project "openshift"
          Use --image-stream="openshift/wildfly:10.1" to specify this image or template

        * Image stream "wildfly" (tag "8.1") in project "openshift"
          Use --image-stream="openshift/wildfly:8.1" to specify this image or template

        * Image stream "wildfly" (tag "9.0") in project "openshift"
          Use --image-stream="openshift/wildfly:9.0" to specify this image or template

        * Image stream "wildfly" (tag "latest") in project "openshift"
          Use --image-stream="openshift/wildfly:latest" to specify this image or template
        ```


        > create new app with specific image

        ```
        oc new-app https://github.com/impradeeparya/datetime-app.git --image-stream="openshift/wildfly:latest"


        --> Found image 3d9426c (6 days old) in image stream "openshift/wildfly" under tag "latest" for "openshift/wildfly:latest"

            WildFly 10.1.0.Final
            --------------------
            Platform for building and running JEE applications on WildFly 10.1.0.Final

            Tags: builder, wildfly, wildfly10

            * The source repository appears to match: jee
            * A source build using source code from https://github.com/impradeeparya/datetime-app.git will be created
              * The resulting image will be pushed to image stream "datetime-app:latest"
              * Use 'start-build' to trigger a new build
            * This image will be deployed in deployment config "datetime-app"
            * Port 8080/tcp will be load balanced by service "datetime-app"
              * Other containers can access this service through the hostname "datetime-app"

            --> Creating resources ...
                imagestream "datetime-app" created
                buildconfig "datetime-app" created
                deploymentconfig "datetime-app" created
                service "datetime-app" created
            --> Success
                Build scheduled, use 'oc logs -f bc/datetime-app' to track its progress.
                Run 'oc status' to view your app.
        ```

    - **Create new application with docker image**

        ```
        oc new-app <DOCKER_IMAGE>
        ```

        **Example**
        ```
        oc new-app impradeeparya/datetime-app:v1
        ```

    - **Create new application with docker file**
        ```
        oc new-app <PROJECT_PATH> --strategy=docker
        ```


6. **Build application**
    ```
    oc start-build <APP_NAME> -n <PROJECT_NAME>
    ```

7. **Delete application**
    - **Delete deployment configuration**
    ```
    oc delete dc <APPLICATION_NAME>
    ```

    - **Delete services**
    ```
    oc delete services <APPLICATION_NAME>
    ```

    - **Delete pod**
    ```
    oc delete pod <APPLICATION_NAME>
    ```

    - **Delete image**
    ```
    oc delete image <IMAGE_NAME>
    ```
8. Reference 
    - [Docker](https://github.com/impradeeparya/docs/blob/master/docker/commands.md)
    - [Jenkins](https://github.com/impradeeparya/docs/tree/master/jenkins)
