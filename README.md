# How To Install GitLab CE on Ubuntu 22.04 
Documentation Link: https://technologyrss.com/how-to-install-gitlab-ce-on-ubuntu-22-04/
youtube link: https://www.youtube.com/watch?v=vU8Nbf85rVA
#### Step01: Server update and upgrade then add repo.
    lsb_release -d && ip r
    apt update && apt upgrade -y
    apt install -y ca-certificates curl openssh-server tzdata
    curl -fsSL https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey| sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/gitlab.gpg
    vi /etc/apt/sources.list.d/gitlab_gitlab-ce.list
    
##### Add below line into source list file.
    deb https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ focal main
    deb-src https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ focal main
#### Step 02: Then run main command.
    apt update
    apt install gitlab-ce
    vi /etc/gitlab/gitlab.rb
#####  Add your server ip address into rb file.
    external_url 'Your Server ip'
#### Step 03: Then configure gitlab-cli
    sudo gitlab-ctl reconfigure
#### Check status using below command.
    gitlab-ctl status
## Collect root password from below command
    cat /etc/gitlab/initial_root_password
###  (Optional) Check below command for manage GitLab.
    gitlab-rake gitlab:check
    gitlab-ctl status
    gitlab-ctl stop
    gitlab-ctl start
    gitlab-ctl restart logrotate
## Configure SSL Certificate for GitLab Server in Ubuntu 20. 04, 22.04 OS
Documentation Link: https://computingforgeeks.com/how-to-secure-gitlab-server-with-ssl-certificate/?expand_article=1

