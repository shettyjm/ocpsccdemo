# Use the Red Hat UBI HTTPD base image
FROM registry.access.redhat.com/ubi8/httpd-24:latest

# Set environment variables for user and group
ENV USERNAME=myhttpduser
ENV USERID=1001
ENV GROUPID=1001

USER root
# Create a group and user with specified UID and GID (if they do not already exist)
RUN groupadd -g ${GROUPID} ${USERNAME} || echo "Group ${USERNAME} already exists" && \
    useradd -u ${USERID} -g ${GROUPID} -m ${USERNAME} || echo "User ${USERNAME} already exists"

# Set the working directory
WORKDIR /usr/share/httpd/html

# Create an index.html file with "Hello, World!"
RUN echo "<!DOCTYPE html><html><head><title>Hello World</title></head><body><h1>Hello, World!</h1></body></html>" > index.html

# Change ownership of files
RUN chown -R ${USERNAME}:${GROUPID} /usr/share/httpd/html

# Switch to the non-root user
USER ${USERNAME}

# Expose the HTTP port
EXPOSE 8080

# Command to run Apache HTTPD
CMD ["httpd", "-D", "FOREGROUND"]
