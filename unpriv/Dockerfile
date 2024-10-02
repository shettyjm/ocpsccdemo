# Use the Red Hat UBI Minimal Nginx base image
FROM registry.access.redhat.com/ubi8/nginx-120:latest

# Set environment variables for user and group
ENV USERNAME=myuser
ENV USERID=1001

# Create a user with specified UID and add to root group (run as root)
USER root

RUN useradd -u ${USERID} -g 0 -m ${USERNAME} || echo "User ${USERNAME} already exists"

# Set the working directory

# Ensure proper permissions for Nginx
RUN chown -R ${USERID}:${USERID} /usr/share/nginx/html && \
    chmod -R 755 /usr/share/nginx/html

WORKDIR /usr/share/nginx/html

# Create a temporary file and then copy it to the Nginx directory
RUN echo "<!DOCTYPE html><html><head><title>Hello World</title></head><body><h1>Hello, World!</h1></body></html>" > /tmp/index.html && \
    cp /tmp/index.html index.html && \
    chown ${USERID}:0 index.html

# Switch to the non-root user
USER ${USERNAME}

# Expose the Nginx default port
EXPOSE 80

# Specify the command to run Nginx
CMD ["nginx", "-g", "daemon off;"]
