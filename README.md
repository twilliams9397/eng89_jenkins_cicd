# Jenkins for CICD
- use Jenkins (open-source automation server) to automate testing and deployment if tests are passed
- create a new SSH key and paste public key into deployment keys in Jenkins repo
![jenkins layout](images/jenkins.png)
- in Jenkins homepage, 'new item' option creates a new job

![jenkins hoome dashboard](images/jenkins_home.png)
- in the freestyle build, check "discard old builds" and set the max number to 3
![freestyle build](images/build_type.png)
![discard](images/discard_builds.png)
- in the build steps select execute shell and type any linux commands here e.g. `uname -a` or `ls -a`
![shell commands](images/execute_shell.png)
- in the project dashboard click 'build now' and select 'view console output' in the menu below to see processes 

![build dashboard](images/build_dashboard.png)
![console output option](images/console_output.png)
- to create a pipeline, select 'trigger other builds' in 'post build actions' and enter the name of the next build in the pipeline - build to be triggered must already be made
![trigger build](images/trigger_pipeline.png)
- for this, the second build has the same configuration but diffetrent shell commands
![second build](images/second_shell.png)
- now when running the first build it will display a message saying the next build has been triggered, which can then be checked/viewed
![first build output](images/first_output.png)
![second build output](images/second_output.png)

## Pipeline for automated testing
- setup a build in the same way as above but with the below options selected as well:
- https of github repo containing the code
![git https](images/pipeline_https_github.png)
- restrict where it can be run
![run area restrict](images/run_node.png)
- source code management, SSH of repo and jenkins key - priv of pair that is in repo, main branch
![jenkins ssh key](images/jenkins_ssh_key.png)
- build environment, ensure correct plugins are checked
![npm env plugin](images/npm_env.png)
- build trigger

![build trigger](images/build_trigger.png)
- shell commands
```linux
cd app
npm install
npm test
```

## Github webhook and merge pipeline
- change branch for above build to dev in source code management
![build to dev branch](images/dev_branch.png)
- after above build, trigger next build to merge dev branch into main branch
### Merge job
- setup the same except:
- don't restrict where project can be run
- branches to build is main, and add this additional behaviour in source code management
![merge behaviours](images/merge_source_code.png)
- in execute shell run following commands:
```linux
git checkout main
git merge origin/dev
```
- setup the following post build action
![merge post build action](images/merge_post_build.png)