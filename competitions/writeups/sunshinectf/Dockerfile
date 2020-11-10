ARG UBUNTU_TAG
FROM ubuntu:${UBUNTU_TAG}

#helpful utilities
COPY --from=busybox /bin/busybox /bin/busybox
RUN cd /bin; for bin in ifconfig iproute traceroute ping less; do ln /bin/busybox /bin/${bin}; done

RUN apt-get update && apt-get install -y  --no-install-recommends \
	build-essential \
	checksec \
	file \
	gdb \
	git \
	libssl-dev \
	libffi-dev \
	ltrace \
	python2 \
	python3 \
	python3-pip \
	python3-dev \
	strace  \
&& \
apt-get autoremove -y && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*
	
RUN python3 -m pip install --upgrade pip && \
	python3 -m pip install --upgrade pwntools

VOLUME /ctf

WORKDIR /ctf

ENTRYPOINT ["/bin/bash"]