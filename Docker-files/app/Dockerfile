# First stage: Build the application using Maven
FROM openjdk:11 AS BUILD_IMAGE

# Install Maven
RUN apt update && apt install -y maven git

# Clone the repository and build the project
RUN git clone https://github.com/Kwamebond/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

# Second stage: Prepare the Tomcat server
FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Bond"

# Remove default webapps and copy the built WAR file from the build stage
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose the necessary port and run Tomcat
EXPOSE 8080
CMD ["catalina.sh", "run"]
