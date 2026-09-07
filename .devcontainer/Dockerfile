
# pull in the python docker image
FROM python:3

# update the container
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
        build-essential \
        curl \
        git \
    && apt-get autoremove --purge -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# add a non-root user based on os user
#   catch the arguments
ARG USERNAME
ARG USER_UID
ARG USER_GID
#   delete if a usr with UID 1000 user exists
RUN if id -u $USER_UID ; then userdel `id -un $USER_UID` ; fi \
#   add and user and setup sudo
    && groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME -s /bin/bash \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# set the default user for the container
USER $USERNAME