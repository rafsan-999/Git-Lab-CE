# How To Install GitLab CE on Ubuntu 22.04 
* Documentation Link: https://technologyrss.com/how-to-install-gitlab-ce-on-ubuntu-22-04/
* youtube link: https://www.youtube.com/watch?v=vU8Nbf85rVA
#### Step01: Server update and upgrade then add repo.
    lsb_release -d && ip r
    apt update && apt upgrade -y
    sudo apt install -y curl openssh-server ca-certificates tzdata
    curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
#### Step 02: Then run main command.
    apt update
    apt install gitlab-ce
#### Step 03: Configure your URL:
Edit the GitLab configuration file to set the your URL for your GitLab instance:

    sudo vi /etc/gitlab/gitlab.rb
#####  Add your server ip address into gitlab.rb file.
    external_url 'http://10.209.99.119'
#### Step 03: Then configure gitlab-cli
    sudo gitlab-ctl reconfigure
## Collect root password from below command
    cat /etc/gitlab/initial_root_password
# Install Specific version of gitlab-ce on Ubuntu:
    sudo EXTERNAL_URL="http://10.209.99.112" apt-get install gitlab-ce=16.3.4-ce.0
## Pin the version to limit auto-updates: 
    sudo apt-mark hold gitlab-ce
## Show what packages are held back: 
    sudo apt-mark showhold

###  (Optional) This is not related in Installation Process Check below command for manage GitLab.
    gitlab-ctl status
    gitlab-ctl start
    gitlab-ctl stop
    gitlab-ctl restart
    gitlab-ctl restart logrotate
    
## Configure SSL Certificate for GitLab Server in Ubuntu 20. 04, 22.04 OS
* Documentation Link: https://computingforgeeks.com/how-to-secure-gitlab-server-with-ssl-certificate/?expand_article=1
* After purchasing your certificate, download the Certificate file and put it with the private key to the /etc/gitlab/ssl/ directory.
    
      /etc/gitlab/ssl/key.pem---your file
      /etc/gitlab/ssl/cert.pem--yor file
     
Then configure SSL settings on your /etc/gitlab/gitlab.rb file. 
* First, change external URL from http to https
* external_url 'https://gitlab.ibos.io.com'
* Under the external_url line paste the below code & save the file
* GitLab NGINX section, enable Nginx and provide SSL key and certificate paths.
* paste it to the vi /etc/gitlab/gitlab.rb file.

      ## GitLab NGINX
      nginx['enable'] = true
      nginx['client_max_body_size'] = '250m'
      nginx['redirect_http_to_https'] = true
            
      nginx['ssl_certificate'] = "/etc/gitlab/ssl/cert.pem"
      nginx['ssl_certificate_key'] = "/etc/gitlab/ssl/key.pem"
      nginx['ssl_protocols'] = "TLSv1.1 TLSv1.2 TLSv1.3"
    
When done, run the following command to effect the changes:

    sudo gitlab-ctl reconfigure
    
Wait for the command to finish executing then visit the URL https://gitlab.ibos.io to Login to your GitLab dashboard.


```sh
# Start all GitLab components
sudo gitlab-ctl start

# Stop all GitLab components
sudo gitlab-ctl stop

# Restart all GitLab components
sudo gitlab-ctl restart









