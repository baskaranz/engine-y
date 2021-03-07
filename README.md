# engine-y

Dockerization of an NGINX server to run on Ubuntu that gets built on Jenkins

## Jenkins [Local] <-> Github
- Jenkins running on local machine exposed on port 8080 for Github webhooks using ngrok secure tunneling

## Jenkins Build Triggers

### Pull Requests to master branch
- GitHub Pull Request Builder plugin on the Jenkins side and webhooks in Github repo
- Builds the NGINX docker image and deploys to dockerhub with build number and latests tags
- Build triggered only when the target branch is master
- Build status is shown on the Pull Request
- This approach doesn't use Jenkinsfile and fully handled by the plugin


```GitHub pull request #35 of commit 8251499c0df5848e891559fbfa186804456f5dd6, no merge conflicts.
Running as SYSTEM
Setting status of 8251499c0df5848e891559fbfa186804456f5dd6 to PENDING with url http://8a7edccb23fa.ngrok.io/job/github-integration-events/25/ and message: 'Build started for merge commit.'
Using context: Jenkins
Building in workspace /var/jenkins_home/workspace/github-integration-events
The recommended git tool is: NONE
using credential githubCred
 > git rev-parse --is-inside-work-tree # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/baskaranz/engine-y.git # timeout=10
Fetching upstream changes from https://github.com/baskaranz/engine-y.git
 > git --version # timeout=10
 > git --version # 'git version 2.20.1'
using GIT_ASKPASS to set credentials 
 > git fetch --tags --force --progress -- https://github.com/baskaranz/engine-y.git +refs/pull/35/*:refs/remotes/origin/pr/35/* # timeout=10
 > git rev-parse refs/remotes/origin/pr/35/merge^{commit} # timeout=10
Checking out Revision ca2ccdb1694fd15bb2d144aebe723050a622095b (refs/remotes/origin/pr/35/merge)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f ca2ccdb1694fd15bb2d144aebe723050a622095b # timeout=10
Commit message: "Merge 8251499c0df5848e891559fbfa186804456f5dd6 into 9e442e0d7211f0f45887b4629204fc2d0502befd"
First time build. Skipping changelog.
Docker Build
Docker Build: building image at path /var/jenkins_home/workspace/github-integration-events
Step 1/10 : FROM ubuntu:20.04


 ---> f63181f19b2f

Step 2/10 : LABEL maintainer="baskaranz@gmail.com"


 ---> Using cache

 ---> f961697fb5c7

Step 3/10 : RUN apt-get update     && apt-get install -y software-properties-common     && apt-add-repository -y ppa:nginx/stable     && apt-get update     && apt-get install -y nginx     && rm -rf /var/lib/apt/lists/*


 ---> Using cache

 ---> bda92816054e

Step 4/10 : ADD nginx/nginx.conf /etc/nginx/nginx.conf


 ---> Using cache

 ---> a601a97fe308

Step 5/10 : ADD nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf


 ---> Using cache

 ---> c91f7aff9da1

Step 6/10 : ADD data/www /data/www


 ---> 33ba1bf6c5f8

Step 7/10 : RUN rm /etc/nginx/sites-enabled/default


 ---> Running in 02223cc98db0

Removing intermediate container 02223cc98db0

 ---> 23536f0ffb6c

Step 8/10 : RUN ln -sf /dev/stdout /var/log/nginx/access.log     && ln -sf /dev/stderr /var/log/nginx/error.log


 ---> Running in e0305e60f437

Removing intermediate container e0305e60f437

 ---> 433c661a895c

Step 9/10 : EXPOSE 80 443


 ---> Running in 6cff90fc03f7

Removing intermediate container 6cff90fc03f7

 ---> 144b11cbd688

Step 10/10 : CMD ["nginx", "-g", "daemon off;"]


 ---> Running in a5144d7f2830

Removing intermediate container a5144d7f2830

 ---> 3b577d587bbe

Successfully built 3b577d587bbe

Tagging built image with beswaran/nginx:25
Tagging built image with beswaran/nginx:latest
Docker Build Response : 3b577d587bbe
Pushing [beswaran/nginx:25, beswaran/nginx:latest]
The push refers to repository [docker.io/beswaran/nginx]
5f22a4b4dc64: Preparing
a69231474b9f: Preparing
06b64003f30a: Preparing
de11e9f8c6c0: Preparing
a0223484f854: Preparing
a8bbf5f91e4d: Preparing
02473afd360b: Preparing
dbf2c0f42a39: Preparing
9f32931c9d28: Preparing
02473afd360b: Waiting
dbf2c0f42a39: Waiting
9f32931c9d28: Waiting
a8bbf5f91e4d: Waiting
06b64003f30a: Pushing [============================>                      ]     512B/904B
06b64003f30a: Pushing [==================================================>]   5.12kB
de11e9f8c6c0: Layer already exists
5f22a4b4dc64: Pushing [==================================================>]     512B
5f22a4b4dc64: Pushing [==================================================>]  3.584kB
a0223484f854: Layer already exists
a69231474b9f: Pushing  3.072kB
a8bbf5f91e4d: Layer already exists
02473afd360b: Layer already exists
9f32931c9d28: Layer already exists
dbf2c0f42a39: Layer already exists
a69231474b9f: Pushed
5f22a4b4dc64: Pushed
06b64003f30a: Pushed
25: digest: sha256:b9a21f36e88979787f0b5fa19cdfa35e674c02857e1f88d1b8b8aaaacd201ca3 size: 2190
The push refers to repository [docker.io/beswaran/nginx]
5f22a4b4dc64: Preparing
a69231474b9f: Preparing
06b64003f30a: Preparing
de11e9f8c6c0: Preparing
a0223484f854: Preparing
a8bbf5f91e4d: Preparing
02473afd360b: Preparing
dbf2c0f42a39: Preparing
9f32931c9d28: Preparing
dbf2c0f42a39: Waiting
a8bbf5f91e4d: Waiting
02473afd360b: Waiting
9f32931c9d28: Waiting
5f22a4b4dc64: Layer already exists
de11e9f8c6c0: Layer already exists
a69231474b9f: Layer already exists
a0223484f854: Layer already exists
06b64003f30a: Layer already exists
dbf2c0f42a39: Layer already exists
02473afd360b: Layer already exists
a8bbf5f91e4d: Layer already exists
9f32931c9d28: Layer already exists
latest: digest: sha256:b9a21f36e88979787f0b5fa19cdfa35e674c02857e1f88d1b8b8aaaacd201ca3 size: 2190
Docker Build Done
Pulling image beswaran/nginx:latest
latest:Pulling from beswaran/nginxnull:Digest: sha256:b9a21f36e88979787f0b5fa19cdfa35e674c02857e1f88d1b8b8aaaacd201ca3null:Status: Image is up to date for beswaran/nginx:latestStarting container for image beswaran/nginx:latest
Started container 3e8079e7fbc0ec437b8f8643586d01c092f0cadc5561adc317682a0e9533bab4
Setting status of 8251499c0df5848e891559fbfa186804456f5dd6 to SUCCESS with url http://8a7edccb23fa.ngrok.io/job/github-integration-events/25/ and message: 'Build finished. '
Using context: Jenkins
Success!

Finished: SUCCESS
```

### Push to a master branch
- Jenkinsfile in the repo is used by Jenkins to build
- NGINX image is built and deployed to dockerhub with build number and latests tags

## TODO
- Docker tests for checking NGINX version and if required config files exist.
