# Cloud-Based-Network-Performance-Testing
Cloud-Based Network Performance Testing

# Cloud-Based Network Performance Testing with LibreSpeed

## Project Overview

This project demonstrates deploying a **cloud-hosted speed test platform** using **Docker containers**. The **LibreSpeed** container image was used to conduct network speed tests efficiently. This setup showcases **containerization**, **network performance monitoring**, and **firewall configurations** in a cloud environment.

---

## 1. Preparing the System and Installing Docker

Before setting up the LibreSpeed container, the system needs to be updated, and Docker must be installed.

### Updating and Upgrading the System:

sudo dnf update  
sudo dnf upgrade  

### Installing Docker:

curl -fsSL https://get.docker.com -o get-docker.sh  
sudo chmod +x get-docker.sh  
./get-docker.sh  

### Adding the Current User to the Docker Group:

sudo usermod -aG docker $USER  

### Enabling, Starting, and Checking Docker Status:

sudo systemctl enable docker  
sudo systemctl start docker  
sudo systemctl status docker  

![Docker Installation](https://via.placeholder.com/600x400?text=Docker+Installation)

---

## 2. Pulling the Docker Image and Configuring the Container

Now, we will pull the **LibreSpeed** container image and configure it with the required settings.

### Pulling the LibreSpeed Docker Image:

sudo docker pull ghcr.io/linuxserver/librespeed  

### Creating a Volume for the Container:

sudo docker volume create librespeed  

### Creating a Network:

sudo docker network create librespeed  

### Creating a Directory for Configuration Files:

sudo mkdir -p /home/fedora/docker/librespeed/config  

### Running the LibreSpeed Container:

docker run -d \  
--name=librespeed \  
-e PUID=1000 \  
-e PGID=1000 \  
-e TZ=America/New_York \  
-p 8080:80 \  
-v /home/fedora/docker/librespeed/config:/config \  
--restart unless-stopped \  
ghcr.io/linuxserver/librespeed  

![Container Creation](https://via.placeholder.com/600x400?text=Container+Creation)  
![Directory Structure](https://via.placeholder.com/600x400?text=Directory+Structure)

---

## 3. Configuring the Firewall

To ensure secure access to the LibreSpeed service, the firewall must be configured to allow necessary ports.

### Installing Firewalld:

sudo dnf install firewalld  

### Enabling and Starting Firewalld:

sudo systemctl enable firewalld  
sudo systemctl start firewalld  

### Adding Required Ports:

sudo firewall-cmd --add-port 8080/tcp --permanent  # LibreSpeed Port  
sudo firewall-cmd --add-port 9000/tcp --permanent  # Portainer (if used)  

### Reloading the Firewall:

sudo firewall-cmd --reload  

![Firewall Configuration](https://via.placeholder.com/600x400?text=Firewall+Configuration)

---

## 4. Verifying and Testing LibreSpeed

Once the container is running, the LibreSpeed web interface can be accessed via:

http://<public-ip>:8080  

You should see the LibreSpeed user interface where you can conduct network speed tests.

![LibreSpeed UI](https://via.placeholder.com/600x400?text=LibreSpeed+UI)

---

## 5. Running a Speed Test

Navigate to the LibreSpeed web interface and run a test. The results should display **download speed, upload speed, latency, and jitter**.

![Speed Test Results](https://via.placeholder.com/600x400?text=Speed+Test+Results)

---

## Conclusion

This project demonstrates the power of **containerization** in deploying lightweight, scalable, and cloud-based applications. The **LibreSpeed** container allows for efficient **network performance testing**, while **Docker and Firewalld configurations** ensure **secure deployment**.

---
