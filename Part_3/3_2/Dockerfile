FROM ubuntu:16.04

ENV LC_ALL=C.UTF-8

RUN apt-get update && apt-get install -y \
	python ffmpeg python-pip wget && \
	pip install yle-dl && \
	rm -rf /var/lib/apt/lists/*
	
WORKDIR /videos	
ENTRYPOINT ["yle-dl"]