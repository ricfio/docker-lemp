FROM alpine:latest

WORKDIR /root

ENTRYPOINT ["bash"]

# INSTALL: bash
#RUN apk --update --no-cache
RUN apk add --no-cache bash

# CUSTOMIZE: .bashrc
RUN echo "export PS1='🐳 \[\033[1;36m\]\h \[\033[1;34m\]\W\[\033[0;35m\] \[\033[1;36m\]# \[\033[0m\]'" >> ~/.bashrc
