######## INSTALL ########

# Set the base image
FROM ubuntu:18.04

# Set environment variables
ENV USER root
ENV HOME /root

# Set working directory
WORKDIR $HOME

# Insert Steam prompt answers
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN echo steam steam/question select "I AGREE" | debconf-set-selections \
 && echo steam steam/license note '' | debconf-set-selections

# Update the repository and install SteamCMD
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y \
 && apt-get install -y --no-install-recommends ca-certificates locales curl \
 && rm -rf /var/lib/apt/lists/*
 
RUN curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf - 

# Add unicode support
RUN locale-gen en_US.UTF-8
ENV LANG 'en_US.UTF-8'
ENV LANGUAGE 'en_US:en'

# Create symlink for executable
#RUN ln -s ./steamcmd.sh /usr/bin/steamcmd

# Update SteamCMD and verify latest version
RUN ./steamcmd.sh +quit

# Set default command
ENTRYPOINT ["./steamcmd.sh"]
CMD ["+help", "+quit"]
