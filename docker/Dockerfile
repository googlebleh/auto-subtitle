FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y \
	curl \
	ffmpeg \
	python3 \
	sudo \
	unzip \
	&& rm -rf /var/lib/apt/lists/*

RUN echo "user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN useradd -m user
USER user
WORKDIR /home/user
ENV PATH="/home/user/.local/bin:$PATH"
RUN curl -LO "https://bootstrap.pypa.io/get-pip.py" \
	&& python3 get-pip.py \
	&& rm get-pip.py

RUN curl -k -LO https://github.com/googlebleh/auto-subtitle/archive/refs/heads/main.zip \
	&& unzip main.zip
WORKDIR /home/user/auto-subtitle-main
RUN python3 -m pip install -r requirements.txt \
	&& python3 setup.py install --user
WORKDIR /home/user
RUN rm -r auto-subtitle-main main.zip
RUN auto_subtitle --help

CMD ["/bin/bash"]
