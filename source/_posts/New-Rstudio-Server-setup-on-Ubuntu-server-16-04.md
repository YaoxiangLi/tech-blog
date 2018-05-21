---
title: New Rstudio Server setup on Ubuntu server 16.04
date: 2018-05-21 16:25:11
tags:
    -Rstudio
    -Linux
    -Ubuntu
    -xcms
categories:
    -Rstudio
---

## update system

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

## update the sources.list to include latest R dist

```bash
sudo sh -c "echo deb https://cloud.r-project.org/bin/linux/ubuntu xenial/ >> /etc/apt/sources.list"
```

## The Ubuntu archives on CRAN are signed with the key of “Michael Rutter marutter@gmail.com” with key ID E084DAB9. To add the key to your system with one command use

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
```

## install R

```bash
sudo apt-get update && sudo apt-get install r-base r-base-dev -y
```

## install xcms dependencies

```bash
sudo apt-get install -y libcurl4-openssl-dev libxml2-dev libssl-dev build-essential software-properties-common libnetcdf-dev
```

## install xcms

```bash
sudo R
```

```r
source("https://bioconductor.org/biocLite.R")
biocLite("xcms")
```

## Install Rstudio server

Install the current version of rstuido server(e.g.v1.1.453)

```bash
sudo apt-get install -y gdebi-core
wget https://download2.rstudio.org/rstudio-server-1.1.453-amd64.deb
sudo gdebi -y rstudio-server-1.1.453-amd64.deb
```

The service in running on default port: 8787
