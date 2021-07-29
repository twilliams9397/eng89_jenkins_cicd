# Jenkins for CICD
- use Jenkins (open-source automation server) to automate testing and deployment if tests are passed
- create a new SSH key and paste public key into deployment keys in Jenkins repo
![jenkins layout](images/jenkins.png)
- in Jenkins homepage, 'new item' option creates a new job
![jenkins hoome dashboard](images/jenkins_home.png)
- in the freestyle build, check "discard old buils" and set the max number to 3
![freestyle build](images/build_type.png)
![discard](images/discard_builds.png)
- in the build steps select execute shell and type any linux commands here e.g. `uname -a` or `ls -a`
![shell commands](images/execute_shell.png)
- in the project dashboard click 'build now' and select 'view console output' to see processes 
![build dashboard](images/build_dashboard.png)
![console output option](images/console_output.png)
- to create a pipeline, select 'trigger other builds' in 'post build actions' and enter the name of the next build in the pipeline - build to be triggered must already be made
![trigger build](images/trigger_pipeline.png)
- for this, the second build has the same configuration but diffetrent shell commands
![second build](images/second_shell.png)
- now when running the first buid it will display a message saying the next build has been triggered, which can then be checked/viewed
![first build output](images/first_output.png)
![second build output](images/second_output.png)