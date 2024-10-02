# Use the Red Hat UBI Minimal Nginx base image
FROM registry.access.redhat.com/ubi8/nginx-120:latest

# Set environment variables for user and group
ENV USERNAME=myuser
ENV GROUPNAME=mygroup
ENV USERID=1001
ENV GROUPID=1001

# Create a group and a user with specified UID and GID
RUN groupadd -g ${GROUPID} ${GROUPNAME} && \
    useradd -u ${USERID} -g ${GROUPNAME} -m ${USERNAME} || true

# Set the working directory
WORKDIR /usr/share/nginx/html

# Create an index.html file with "Hello, World!"
RUN echo "<!DOCTYPE html><html><head><title>Hello World</title></head><body><h1>Hello, World!</h1></body></html>" > index.html

# Change ownership of the application files
RUN chown -R ${USERID}:${GROUPID} /usr/share/nginx/html

# Switch to the non-root user
USER ${USERNAME}

# Expose the Nginx default port
EXPOSE 80

# Specify the command to run Nginx
CMD ["nginx", "-g", "daemon off;"]
