#Using Ubuntu latest imaage
FROM ubuntu:latest

#Run update
RUN apt-get update

#Install Java
RUN apt install software-properties-common apt-transport-https -y
RUN add-apt-repository ppa:openjdk-r/ppa -y
RUN apt install openjdk-8-jdk -y
RUN java -version

#Install jenkins
RUN wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
RUN echo 'deb https://pkg.jenkins.io/debian-stable binary/' | tee -a /etc/apt/sources.list
RUN apt-get update 
RUN apt install jenkins -y
RUN systemctl start jenkins
RUN systemctl enable jenkins

#Install Appache
RUN apt install apache2 -y
RUN a2enmod proxy
RUN a2enmod proxy_http
COPY * /etc/apache2/sites-available/
RUN a2ensite jenkins
RUN systemctl restart apache2
RUN systemctl restart jenkins

#Install Configure UFW Firewall
RUN ufw allow ssh  
RUN ufw allow http
RUN ufw allow https
RUN ufw allow 8080
RUN ufw enable

EXPOSE 8080