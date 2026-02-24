Commands (pre-requsits before making this Linux vm as a self-hosted agent for out azure devops pipeline):


#1 - to do ...
sudo apt update 

#2 - install docker
sudo apt install docker.io

#3 - give permission to the logged in user(azureuser)
sudo usermod -aG docker azureuser

#4 - restart docker
sudo systemctl restart docker

#5 - connect back to vm
exit
ssh -i <keyfile> username@<IP address of VM>

#6 - test if logged in user can work with docker
docker pull hello-world