# Run Brave Browser in a Container
#
# docker run -it \
#       --net host \
#       --cpuset-cpus 0 \
#       --memory 512mb \
#       -v /tmp/.X11-unix:/tmp/.X11-unix \
#       -e DISPLAY=unix$DISPLAY \
#       -v $HOME/Downloads:/home/brave/Downloads:rw \
#       -v $HOME/.config/BraveSoftware/Brave-Browser/:/data/:rw \
#       --security-opt seccomp=$HOME/brave.json \
#       --device /dev/snd \
#       --device /dev/dri \
#       -v /dev/shm:/dev/shm \
#       --name brave-browser \
#       nasirhm/brave-browser:beta
#
# You will want the custom seccomp profile:
#     wget https://raw.githubusercontent.com/nasirhm/dotfiles/main/etc/docker/seccomp/brave.json -o ~/brave.json

# Base docker image
FROM debian:bullseye-slim
LABEL maintainer "Nasir Hussain <nasirhussainm14@gmail.com>"

# Install Brave Browser
RUN apt update && apt-get install -y \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg \
        hicolor-icon-theme \
        libcanberra-gtk* \
        libgl1-mesa-dri \
        libgl1-mesa-glx \
        libpangox-1.0-0 \
        libpulse0 \
        libv4l-0 \
        fonts-symbola \
        --no-install-recommends \
        && curl -ssl https://brave-browser-apt-beta.s3.brave.com/brave-core-nightly.asc | apt-key add - \
        && echo "deb [arch=amd64] https://brave-browser-apt-beta.s3.brave.com/ stable main" > /etc/apt/sources.list.d/brave-browser-beta.list \
        && apt-get update && apt-get install -y \
        brave-browser-beta \
        --no-install-recommends \
        && apt-get purge --auto-remove -y curl \
        && rm -rf /var/lib/apt/lists/*

# Add brave user
RUN groupadd -r brave && useradd -r -g brave -G audio,video brave \
    && mkdir -p /home/brave/Downloads && chown -R brave:brave /home/brave

# Run Brave as a non privileged user
USER brave

# Autorun brave-browser
ENTRYPOINT [ "brave-browser-beta" ]
CMD [ "--user-data-dir=/data" ]