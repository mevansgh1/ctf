ARG UBUNTU_TAG
FROM ubuntu:${UBUNTU_TAG}

ARG DEBIAN_FRONTEND=noninteractive

#helpful utilities
COPY --from=busybox /bin/busybox /bin/busybox
RUN cd /bin; for bin in ifconfig iproute traceroute ping less wget; do ln /bin/busybox /bin/${bin}; done

RUN apt-get update && apt-get install -y  --no-install-recommends \
	apt-transport-https \
	build-essential \
	checksec \
	curl \
	file \
	gdb \
	git \
	gnupg-agent \
	libssl-dev \
	libffi-dev \
	ltrace \
	python2 \
	python3 \
	python3-pip \
	python3-dev \
	software-properties-common \
	strace  \
&& \
apt-get autoremove -y && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*

# Install pwn tools	
RUN python3 -m pip install --upgrade pip && \
	python3 -m pip install --upgrade pwntools

# Install docker cli

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
	&& apt-key fingerprint 0EBFCD88 \
	&& add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs) stable" \
   	&& apt-get update \
   	&& apt-get install -y docker-ce-cli

VOLUME /ctf

WORKDIR /ctf

ENTRYPOINT ["/bin/bash"]