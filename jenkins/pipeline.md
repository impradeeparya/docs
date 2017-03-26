# Jenkins CI CD pipeline setup

1. Click on jenkins(top left corner) then Goto Manage jenkins->Manage plugins
2. Two way to install **build pipeline** plugin

    - Goto to Available tab and search for **build pipeline** plugin, select it and install it.

      ![alt tag](https://cloud.githubusercontent.com/assets/8745622/23723664/0351810e-0470-11e7-8c75-10a0da670fbb.png)

    - [Download](http://mirrors.jenkins-ci.org/plugins/) build pipeline plugin and Goto Advanced tab, choose downloaded plugin file(.hpi) in upload plugin section and click on upload button to install.

      ![alt tag](https://cloud.githubusercontent.com/assets/8745622/23723718/3af1cbc8-0470-11e7-9ef0-6a4f3b9dc3a7.png)

    - Follow same steps to install **pipeline plugin**

3. Now Goto Home page of jenkins and click on New Item to create build pipeline
4. Enter Item name and select pipeline from below given projects and then click ok.

    ![alt tag](https://cloud.githubusercontent.com/assets/8745622/23725696/8f66b784-0477-11e7-8ad8-476938138d09.png)

5. Fill configuration according to requirements and press OK.

    ![alt tag](https://cloud.githubusercontent.com/assets/8745622/24329786/689760b2-122e-11e7-8e29-3d97e486a750.png)
    
    ![alt tag](https://cloud.githubusercontent.com/assets/8745622/24329803/c1ce5afa-122e-11e7-9d64-37f0942273f5.png)
    
6. Click on run of pipeline view page to run pipeline.

    ![alt tag](https://cloud.githubusercontent.com/assets/8745622/24329817/1e65afa2-122f-11e7-9cdb-dcf84144f6bc.png)
    
    - Green  : success
    - Yellow : Running or build finished with warning
    - Red    : Failed
    
7. Configure deployment step. Create another job for pipeline that will deploy war to particular server.
8. Create job by clicking NEW_ITEM on jenkins home page or click on add step in pipeline view and configure deploy steps.

    ![alt tag](https://cloud.githubusercontent.com/assets/8745622/24330140/f5feb80e-1235-11e7-80cb-645eaeeae6d2.png)
    
9. Click run on pipeline to trigger all jobs or steps of pipeline in sequence.

    ![alt tag](https://cloud.githubusercontent.com/assets/8745622/24330143/02bf581e-1236-11e7-87a9-626b480a9d00.png)
    
>If build and deploy jobs are running in different nodes then in that case we can't copy war in deploy step from build workspace as there workspaces are different. So in this case copy war in some snapshot repository(like NEXUS) at the time of build and then download it at the time of deployment.
  
10. Deployment can be done in following ways : 
    - Copy war to given server through SCP and then restart server.
    - Openshift [Apass](https://github.com/impradeeparya/docs/blob/master/openshift/commands.md)
    
    >There are many ways to deploy our code to server but as of now i dirty my hands with above two ways only.