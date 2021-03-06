# Use an official Python runtime as a parent image
#FROM python:2.7-slim
FROM alpine:latest
# FROM ubuntu:latest
MAINTAINER Patrowl.io "getsupport@patrowl.io"
LABEL Name="Nessus\ \(Patrowl engine\)" Version="1.0.0"

# Set the working directory
RUN mkdir -p /opt/patrowl-engines/nessus
RUN mkdir -p /opt/patrowl-engines/nessus/results
RUN mkdir -p /opt/patrowl-engines/nessus/reports
WORKDIR /opt/patrowl-engines/nessus

# Copy the current directory contents into the container at /
COPY __init__.py .
COPY engine-nessus.py .
COPY nessus.json.sample nessus.json
COPY requirements.txt .
COPY README.md .
COPY etc/ ./etc/

# RUN apk add nmap --no-cache && rm -f /var/cache/apk/*
RUN apk add --update \
    python \
    python-dev \
    py-pip \
  && rm -rf /var/cache/apk/*
RUN pip install --upgrade pip
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# TCP port exposed by the container (NAT)
EXPOSE 5102

# Run app.py when the container launches
CMD ["python", "engine-nessus.py"]
