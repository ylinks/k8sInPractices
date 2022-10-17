# k8sInPractices
Notes and others things about k8s

## Installing Docker in Windows without Docker Desktop
[Source](https://www.knulst.de/how-to-install-docker-without-docker-desktop-on-windows/) knulst.de

You can also install the Linux Subsystem with a PowerShell command:

Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
Install Ubuntu on WSL2
After you set up the prerequisite you have to open a PowerShell with administrative privileges and install Ubuntu in WSL2 with the following command:

wsl --set-default-version 2
wsl --install -d Ubuntu
You can also install different Linux submodules within this step.

After the installation is finished you should check if Ubuntu was installed in the correct version:

wsl -l -v
If everything worked correctly you should see your installed Ubuntu with the corresponding WSL version. If the version is not correct you can change it with:

wsl --set-version Ubuntu-YY.MM 2
YY.MM is the version of the Ubuntu version that you installed recently.

Install Docker
To install Docker on Windows within the Ubuntu submodule you can follow the official steps for installing Docker on Ubuntu:

https://docs.docker.com/engine/install/ubuntu/
Another way will be to create a new file and copy the following script into it. These commands are only copied from the official tutorial into a file to share with fellow developers

#/bin/bash 

# 1. Required dependencies 
sudo apt-get update 
sudo apt-get -y install apt-transport-https ca-certificates curl gnupg lsb-release 

# 2. GPG key 
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg 

# 3. Use stable repository for Docker 
echo \ 
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \ 
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 

# 4. Install Docker 
sudo apt-get update 
sudo apt-get -y install docker-ce docker-ce-cli containerd.io 

# 5. Add user to docker group 
sudo groupadd docker 
sudo usermod -aG docker $USER 
Switch to your Ubuntu submodule within PowerShell and execute the file to install Docker and the needed dependencies.

