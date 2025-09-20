# JENKINS-CI-CD-_PROJECT
Jenkins on AWS EC2 for CI + Tomcat on AWS EC2 for CD, using a Maven project (pom.xml). It’s structured like a real-world DevOps project.

# 🚀 Jenkins CI + Tomcat CD with Maven on AWS EC2

This project sets up a **CI/CD pipeline** where **Jenkins (on AWS EC2)** handles Continuous Integration (CI) and **Apache Tomcat (on AWS EC2)** manages Continuous Deployment (CD).  
The application is built with **Maven**, tested via Jenkins, and deployed automatically to a **Tomcat server** hosted on EC2.

## 📂 Project Repository
- Git Repo (with `pom.xml`): [datapromaven](https://github.com/teluguhackerforfree/datapromaven.git)
- 
## ⚙️ Infrastructure & Tech Stack
- **AWS EC2** → Hosts Jenkins & Tomcat servers  (ubuntu)
- **Jenkins** → CI automation  
- **Maven** → Build & dependency management  
- **Java JDK 11/17** → Application runtime  
- **Apache Tomcat** → Deployment server for `.war`  
- **GitHub** → Source control
- 
## 🔄 Pipeline Flow
1. **Checkout** → Jenkins pulls code from Git repo.  
2. **Build** → Maven compiles + resolves dependencies with `pom.xml`.  
3. **Test** → Runs unit tests inside Jenkins.  
4. **Package** → Generates `.war` file inside `target/`.  
5. **Deploy** → Jenkins uploads `.war` to Tomcat running on EC2.
   
   
 <img width="1200" height="517" alt="jenkins proj" src="https://github.com/user-attachments/assets/0598f72a-3d72-4a7a-86dd-829d7e8662dc" />
 
## ☁️ AWS Setup

### 1️⃣ Launch EC2 Instances
- **Instance 1 (Jenkins Server(ci))** → Install Jenkins, Maven, Git, Java  
- **Instance 2 (Tomcat Server(cd))** → Install Java, Apache Tomcat  

### 2️⃣ Install Jenkins on EC2


```bash
# Connect to EC2
ssh -i your-key.pem ubuntu@<jenkins(ci)-ec2-ip>

# Install Java, Maven, Git
sudo apt update && sudo apt install openjdk-11-jdk maven git -y

# Install Jenkins

wget https://get.jenkins.io/war-stable/2.516.3/jenkins.war
check:ls
java -jar jenkins.war


# Access Jenkins at: http://<jenkins-ec2-ip>:8080

3️⃣ Install Tomcat on EC2

ssh -i your-key.pem ubuntu@<tomcat(cd)-ec2-ip>
sudo apt update && sudo apt install openjdk-11-jdk wget -y

# Install Tomcat
sudo apt update
sudo apt-get install -y tomcat9
sudo apt-get install -y tomcat9-admin
cd /etc/tomcat9
ls
sudo vi tomcat-user.xml
<user username="jenkins" password="VISHNU"
roles="manager-script,manager-status,manager-gui"/> 
 
sudo service tomcat9 restart
Tomcat runs at: http://<tomcat-ec2-ip>:8080

4️⃣ Configure Tomcat for Remote Deployment

Edit tomcat-users.xml:

<user username="jenkins" password="VISHNU"
roles="manager-script,manager-status,manager-gui"/>


Restart Tomcat:

sudo service tomcat9 restart

📊 Outputs

Build Logs → Jenkins Console Output

Artifacts → .war in target/

Deployed App → Accessible at:

http://<tomcat-ec2-ip>:8080/jenkins.project



🌟 Benefits

Cloud-based CI/CD with AWS scalability

Automated builds + deployments

Seamless integration with GitHub + Maven

Reproducible and reliable delivery pipeline
  
