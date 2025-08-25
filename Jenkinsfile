Started by user Komal

Obtained Jenkinsfile from git https://github.com/Dhanvikah/node-bulletin-board.git
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins
 in /var/jenkins_home/workspace/CICD
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Declarative: Checkout SCM)
[Pipeline] checkout
Selected Git installation does not exist. Using Default
The recommended git tool is: NONE
using credential Docker-creds
 > git rev-parse --resolve-git-dir /var/jenkins_home/workspace/CICD/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/Dhanvikah/node-bulletin-board.git # timeout=10
Fetching upstream changes from https://github.com/Dhanvikah/node-bulletin-board.git
 > git --version # timeout=10
 > git --version # 'git version 2.39.5'
using GIT_ASKPASS to set credentials 
 > git fetch --tags --force --progress -- https://github.com/Dhanvikah/node-bulletin-board.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
Checking out Revision 432482fb8d95921475a4a40a9b4cc13efa3f597b (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 432482fb8d95921475a4a40a9b4cc13efa3f597b # timeout=10
Commit message: "chore: updated Jenkinsfile and moved Dockerfile inside bulletin-board-app"
 > git rev-list --no-walk 7116d8ac8d9338a8e08e83d6228d96a88e6f939a # timeout=10
[Pipeline] }
[Pipeline] // stage
[Pipeline] withEnv
[Pipeline] {
[Pipeline] withCredentials
Masking supported pattern matches of $DOCKERHUB_CREDENTIALS or $DOCKERHUB_CREDENTIALS_PSW or $GITHUB_CREDS or $GITHUB_CREDS_PSW
[Pipeline] {
[Pipeline] withEnv
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Checkout)
[Pipeline] checkout
Selected Git installation does not exist. Using Default
The recommended git tool is: NONE
using credential Docker-creds
 > git rev-parse --resolve-git-dir /var/jenkins_home/workspace/CICD/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/Dhanvikah/node-bulletin-board.git # timeout=10
Fetching upstream changes from https://github.com/Dhanvikah/node-bulletin-board.git
 > git --version # timeout=10
 > git --version # 'git version 2.39.5'
using GIT_ASKPASS to set credentials 
 > git fetch --tags --force --progress -- https://github.com/Dhanvikah/node-bulletin-board.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
Checking out Revision 432482fb8d95921475a4a40a9b4cc13efa3f597b (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 432482fb8d95921475a4a40a9b4cc13efa3f597b # timeout=10
Commit message: "chore: updated Jenkinsfile and moved Dockerfile inside bulletin-board-app"
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Build Docker image)
[Pipeline] script
[Pipeline] {
[Pipeline] sh
+ docker build -t komall6/node-bulletin-board:20-432482f -t komall6/node-bulletin-board:latest -f bulletin-board-app/Dockerfile bulletin-board-app
#1 [internal] load build definition from Dockerfile
#1 sha256:e9264679513ea85f85935c16e92279018ac60168fd809a94dead0fa2ba519ab7
#1 transferring dockerfile: 248B done
#1 DONE 0.0s

#3 [auth] library/node:pull token for registry-1.docker.io
#3 sha256:7576c9e44fcbf0c97d9ff5a0db0736069d0e1316881ac0b71a7185c798c1353c
#3 DONE 0.0s

#2 [internal] load metadata for docker.io/library/node:18-alpine
#2 sha256:fb90574236a0a1e8fa4d18b0da9ea146d2e7739e0b128b5c0407af25bc742abc
#2 DONE 2.8s

#4 [internal] load .dockerignore
#4 sha256:de640bb281715c760d7431666831f4c3f21bea277c2e72ebd94502d8edc37bb7
#4 transferring context: 2B done
#4 DONE 0.0s

#8 [internal] load build context
#8 sha256:6bfbab018b96e72fff9ecc43f49094a56c56a8517468da2b0c297be7efbc2b0b
#8 transferring context: 519B done
#8 DONE 0.0s

#10 [1/5] FROM docker.io/library/node:18-alpine@sha256:8d6421d663b4c28fd3ebc498332f249011d118945588d0a35cb9bc4b8ca09d9e
#10 sha256:f91489ef195421a94c9aefb08af26be78585273fab4a49f12a8cf6d7551aa80f
#10 resolve docker.io/library/node:18-alpine@sha256:8d6421d663b4c28fd3ebc498332f249011d118945588d0a35cb9bc4b8ca09d9e 0.0s done
#10 DONE 0.0s

#9 [2/5] WORKDIR /usr/src/app
#9 sha256:2895ac04dc87b9a3eb99ae369a55231fc9528f5c8d85a5f417ff66d6cfab7c88
#9 CACHED

#6 [4/5] RUN npm install --only=production
#6 sha256:35f540ffb882fa3c996fcd1078833bf819a294424f48270c526a18f4c16967e9
#6 CACHED

#7 [3/5] COPY package*.json ./
#7 sha256:4b35931aa847d75110bbde34e2427af7b13dcfed3ad5a7df382334fcf8565509
#7 CACHED

#5 [5/5] COPY . .
#5 sha256:1b7d3899af7b95c25d9e05245170feb7f1e5e2fa54b2ca239d5b8fbab522523b
#5 CACHED

#11 exporting to image
#11 sha256:1b162ef436b90793c903c09971e9339a65be5d6a1f54e4eb523beb9b2fb9986e
#11 exporting layers done
#11 exporting manifest sha256:3630ce83c56b6afbef7841d02d8d5a1b69a878eef04afe0782e51155061aba25 done
#11 exporting config sha256:59234b67966753abd14a33609ee73b7eba82d4f5091e6bad2be46a5cb3951978 done
#11 naming to docker.io/komall6/node-bulletin-board:20-432482f done
#11 unpacking to docker.io/komall6/node-bulletin-board:20-432482f done
#11 naming to docker.io/komall6/node-bulletin-board:latest done
#11 unpacking to docker.io/komall6/node-bulletin-board:latest done
#11 DONE 1.4s
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Push Docker image)
[Pipeline] withCredentials
Masking supported pattern matches of $DOCKER_PASS
[Pipeline] {
[Pipeline] sh
+ echo ****
+ docker login -u komall6 --password-stdin
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
[Pipeline] sh
+ docker push komall6/node-bulletin-board:20-432482f
The push refers to repository [docker.io/komall6/node-bulletin-board]
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
5045b7b6efda: Layer already exists
18924916c807: Layer already exists
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
f18232174bc9: Waiting
25ff2da83641: Waiting
dd71dde834b5: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
6e111d656bae: Waiting
1e5a4c89cee5: Waiting
ed1ca1f013bf: Waiting
f18232174bc9: Waiting
25ff2da83641: Layer already exists
dd71dde834b5: Waiting
dd71dde834b5: Waiting
6e111d656bae: Layer already exists
1e5a4c89cee5: Layer already exists
ed1ca1f013bf: Waiting
f18232174bc9: Waiting
ed1ca1f013bf: Waiting
f18232174bc9: Waiting
dd71dde834b5: Layer already exists
ed1ca1f013bf: Layer already exists
f18232174bc9: Layer already exists
20-432482f: digest: sha256:3630ce83c56b6afbef7841d02d8d5a1b69a878eef04afe0782e51155061aba25 size: 1876
[Pipeline] sh
+ docker push komall6/node-bulletin-board:latest
The push refers to repository [docker.io/komall6/node-bulletin-board]
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
1e5a4c89cee5: Layer already exists
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
18924916c807: Layer already exists
6e111d656bae: Waiting
dd71dde834b5: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
25ff2da83641: Waiting
5045b7b6efda: Waiting
f18232174bc9: Waiting
6e111d656bae: Waiting
25ff2da83641: Layer already exists
5045b7b6efda: Layer already exists
f18232174bc9: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Waiting
6e111d656bae: Waiting
dd71dde834b5: Waiting
ed1ca1f013bf: Layer already exists
f18232174bc9: Waiting
f18232174bc9: Waiting
6e111d656bae: Layer already exists
dd71dde834b5: Waiting
dd71dde834b5: Layer already exists
f18232174bc9: Layer already exists
latest: digest: sha256:3630ce83c56b6afbef7841d02d8d5a1b69a878eef04afe0782e51155061aba25 size: 1876
[Pipeline] }
[Pipeline] // withCredentials
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Update Helm values & push to Git)
[Pipeline] dir
Running in /var/jenkins_home/workspace/CICD/helm
[Pipeline] {
[Pipeline] withCredentials
Masking supported pattern matches of $GIT_TOKEN
[Pipeline] {
[Pipeline] script
[Pipeline] {
[Pipeline] sh
+ sed -i s/tag: .*/tag: "20-432482f"/ values.yaml
[Pipeline] sh
+ git config user.email jenkins@ci.local
+ git config user.name jenkins
[Pipeline] sh
+ git add values.yaml
+ git commit -m ci: bump image tag to 20-432482f
[detached HEAD 50dc152] ci: bump image tag to 20-432482f
 1 file changed, 1 insertion(+), 1 deletion(-)
[Pipeline] sh
+ git rev-parse --abbrev-ref HEAD
[Pipeline] sh
+ git symbolic-ref refs/remotes/origin/HEAD
+ sed s@^refs/remotes/origin/@@
fatal: ref refs/remotes/origin/HEAD is not a symbolic ref
[Pipeline] sh
Warning: A secret was passed to "sh" using Groovy String interpolation, which is insecure.
		 Affected argument(s) used the following variable(s): [GIT_TOKEN, GITHUB_CREDS_PSW, GITHUB_CREDS]
		 See https://jenkins.io/redirect/groovy-string-interpolation for details.
+ echo -n Dhanvikah:****
+ base64
+ git -c http.extraHeader=AUTHORIZATION: basic RGhhbnZpa2FoOk**** push origin HEAD:
fatal: invalid refspec 'HEAD:'
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // withCredentials
[Pipeline] }
[Pipeline] // dir
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Trigger ArgoCD Sync)
Stage "Trigger ArgoCD Sync" skipped due to earlier failure(s)
[Pipeline] getContext
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // withCredentials
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
ERROR: script returned exit code 128
Finished: FAILURE
