FROM registry.fedoraproject.org/fedora:38
MAINTAINER copr-devel@lists.fedorahosted.org

RUN dnf -y update && \
    # Base packages
    dnf -y install htop \
                   make \
                   wget \
                   net-tools \
                   iputils \
                   vim \
                   mlocate \
                   git \
                   sudo \
                   python3-ipdb \
                   findutils \
    # The dependencies for this project
    && dnf -y install \
                   npm \
                   java \
    && dnf clean all

# We cannot use volumes to bindmount code from the host during the build phase.
# We need to copy them.
COPY ./ /src/code/

WORKDIR /src/code/frontend
RUN npm install
RUN npm install -g shadow-cljs

# Unintuitive command but it downloads all ClojureScript dependencies
# https://github.com/thheller/shadow-cljs/issues/362
RUN npx shadow-cljs classpath
