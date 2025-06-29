## Django Web App Deployment

###  Steps to Run the Project

#### 1. **Create an EC2 Instance**

* Launch an Ubuntu instance on AWS.
* Ensure the security group allows SSH (port 22) and **custom TCP port 8000** (added later).

#### 2. **Install Docker**

```bash
sudo apt update
sudo apt install -y docker.io
```



#### 3. **(Optional) Edit the HTML Template**

If you want to modify the frontend HTML:

```bash
cd devops/demo/templates
nano index.html  # or use any editor like vim
```

Make your changes and save the file.

#### 6. **Switch Back to App Directory**

```bash
cd ~/Django-web-app
```

#### 6. **Add Current User to Docker Group**

```bash
sudo usermod -aG docker $USER
```

#### 7. **Logout and Login Again**

* This is required to apply Docker group changes.

#### 8. **Refresh Docker Group in Current Shell**

```bash
newgrp docker
```

#### 9. **Build Docker Image**

```bash
docker build -t python-web-app .
```

#### 10. **Verify Image is Built**

```bash
docker images
```

#### 11. **Run Docker Container**

```bash
docker run -p 8000:8000 -it python-web-app
```
![image](https://github.com/user-attachments/assets/2bc1feae-2a40-4f97-a755-681f532fb605)

#### 12. **Update EC2 Security Group**

* Go to AWS Console → EC2 → Security Groups.
* Add **Inbound Rule**:

  * Type: Custom TCP
  * Port: `8000`
  * Source: `0.0.0.0/0` or your IP

#### 13. **Access the Web App**

* Open your browser and go to:
  **`http://<your-ec2-public-ip>:8000`**

![image](https://github.com/user-attachments/assets/25fb36e2-c1d9-490c-9aff-a345b90c3a4b)


### 🎉 Done!

You now have a Python web app running in Docker on your EC2 instance.
