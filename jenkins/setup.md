# Jenkins build pipeline setup

1. [Download](https://jenkins.io/) jenkins war.
2. Copy it to apache tomcat webapps folder and then start apache tomcat server.
3. Hit http://localhost:8080/jenkins/ url on browser you will get below screen.

    > ![alt tag](https://cloud.githubusercontent.com/assets/8745622/23674782/173006d8-039d-11e7-8ff9-8ea9c3de21f6.png)

4. Skip this step as of now and close this **Customize jenkins** popup.
5. Below is the home page of jenkins

    > ![alt tag](https://cloud.githubusercontent.com/assets/8745622/23675167/77cbe574-039e-11e7-98ad-b9eac390d386.png)

6. Now click on **New item** and enter the name of the job. As of now there is no extra plugin installed to create different types of project, so create it as freestyle project and press OK.

    > ![alt tag](https://cloud.githubusercontent.com/assets/8745622/23675422/4e477ba4-039f-11e7-8e8e-57239b9b31f1.png)

7. Below is the configuration page of above created job.

    > ![alt tag](https://cloud.githubusercontent.com/assets/8745622/23675656/07485b1e-03a0-11e7-87b4-dc4afdeaf434.png)

8. As above images shows None in **Source Code Management** part of configurations, we need to install git plugin if we want to use git as **SCM**.
9. Click on Jenkins(Top left corner), Goto **Manage Jenkins->Manage Plugins**.
10. Goto Available tab, search for **Git plugin**, select it and click on download install restart.
11. After installing and restarting jenkins, click on job created above on home page of jenkins and then click on configure you will get back to same configuration page of you above created job.
12. Goto SCM part of configuration, select GIT and add you git repo url.

    > ![alt tag](https://cloud.githubusercontent.com/assets/8745622/23676677/740e0232-03a3-11e7-9b6a-eec2cd512fc3.png)

13. Goto to above created job page and click on **Build Now**.
