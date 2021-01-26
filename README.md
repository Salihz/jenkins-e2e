# maven-project

Simple Maven Project

Jenkins Installation
1. Spin up EC2 instance
2. sudo su -
3. vi /etc/hostname --> change value to jenkins-node
4. hostname jenkins-node --> exit and log back in
5. Install Java --> Verify Java is installed or not --> java -version
6. yum install java-1.8* -y
7. find /usr/lib/jvm/java-1.8* | head -n 3
8. ls -l /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.amzn2.0.1.x86_64/jre/
9. cd ~ --> Go back to home of root user
10. vi .bash_profile
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
	. ~/.bashrc
fi

# User specific environment and startup programs

JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.amzn2.0.1.x86_64
PATH=$PATH:$HOME/bin:$JAVA_HOME

export PATH

11. cat /etc/*-release --> Find out linux distro
12. Google for Jenkins Download --> Pick LTS(Long Term Support) --> Rhel,Centos,Fedora -->
13. wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
14. rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
15. yum install jenkins -y
16. service jenkins  start
17. grab publichIP of Jenkins VM and paste to browser and port number 8080 --> XXXXXXXXXX:8080
18. Copy /var/lib/jenkins/secrets/initialAdminPassword and in Jenkins box --> cat /var/lib/jenkins/secrets/initialAdminPassword
19. Install suggested plugins --> Next --> Add your credentials


Working with Jenkins
1. Configure JDK in Jenkins GUI --> Manage Jenkins --> Global Tool Configuration --> Add JDK --> Name: JAVA_HOME -->
go to Jenkins Box (Terminal/CMD) and run echo $JAVA_HOME --> Copy the output and paste under JAVA_HOME
2. Build Job --> New Item --> Freestyle Project --> Description --> Build Actions --> Execute Shell --> echo "Welcome to Cloudiar"
--> Build Now.

Building CI/CD pipeline
1. Install git --> yum install git -y
2. Jenkins GUI --> Manage Jenkins --> Manage Plugins --> Available --> Filter: GitHub Integration --> Install Without Restart
3. Manage Jenkins --> Global Tool Configuration --> Change Default to GitHub and save

Install Maven  (Build Management Tool)
1. Google for Maven Download
2. Right Click on "apache-maven-3.6.3-bin.tar.gz" and copy link address
3. Jenkins box --> cd /opt --> wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
4. tar -xvzf apache-maven-3.6.3-bin.tar.gz
5. mv apache-maven-3.6.3 maven --> Creates user friendly folder name
6. cd ~
7. vi .bash_profile
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
	. ~/.bashrc
fi

# User specific environment and startup programs

JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.amzn2.0.1.x86_64
M2_HOME=/opt/maven
M2=$M2_HOME/bin
PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2:$M2_HOME

export PATH

8. exit from Jenkins Box and log back in (sudo su -)
9. echo $M2 and echo $M2_HOME
10. Jenkins GUI --> Manage Jenkins --> Manage Plugins --> Available --> Maven Invoker
11. Cloned with SSH as project is private: git@github.com:Salihz/jenkins-e2e.git

If SSH is not authenticated than clone HTTPS public.
Jenkins box --> git clone https://github.com/Salihz/jenkins-e2e.git
12. cd hello-cloudiar
13. yum install tree -y
