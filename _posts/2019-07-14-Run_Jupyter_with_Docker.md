---
layout: post
title: "Docker를 이용한 Jupyter 실행하기"
date: 2019-07-14
categories: blog
tags: python jupyter docker
comments: true
---
최근 회사에서 [Python](https://www.python.org) 기본 교육을 받았는데 Python 에디터로 [Jupyter](https://jupyter.org)를 사용하였다. 교육을 받을때는 Python 개발 환경 구성을 위해 교육용 PC에 [Anaconda](https://www.anaconda.com)를 설치하고 Anaconda 내에서 Jupyter Notebook을 실행 했었는데, [Docker](https://www.docker.com)를 이용하면 이런 저런 설치 없이 간단하게 Jupyter를 사용할 수 있는 Python 개발 환경을 구성할 수 있다.

Docker를 이용해 Jupyter를 실행하는 방법은 여러가지가 있을 수 있겠지만, 여기서는 Anaconda 이미지를 이용하여 Jupyter Notebook을 실행하는 방법과 Jupyter 이미지를 이용하여 Jupyter Lab을 실행하는 방법을 소개한다. Docker를 이용하므로 Docker는 당연히 설치되어 있어야 한다.

### 방법 1. Anaconda 이미지를 이용하는 방법

Anaconda3 Docker 이미지 가져오기

```bash
$ docker pull continuumio/anaconda3
```

Anaconda3 컨테이너 실행

```bash
$ docker run --rm -p 8888:8888 -v $(pwd):/notebooks -it continuumio/anaconda3 /bin/bash
```

실행중인 컨테이너 내부에서 Jupyter Notebook 실행

```bash
# in the anaconda container
$ jupyter notebook --ip='0.0.0.0' --port=8888 --no-browser --allow-root
```

Jupyter Notebook 실행 정보가 표시된 후 마지막에 접속 경로가 `http://<호스트>:8888/?token=<토큰 문자열>`과 같은 형태로 표시된다. 

해당 URL을 복사하여 Docker 컨테이너가 실행 중인 PC의 브라우저 주소창에 `http://localhost:8888/?token=<토큰 문자열>`을 입력하면 Jupyter Notebook이 실행된 것을 확인할 수 있다.

### 방법 2. Jupyter 이미지를 이용하는 방법

Jupyter 이미지 가져오기

```bash
$ docker pull jupyter/datascience-notebook
```

Jupyter 컨테이너 실행

```bash
$ docker run --rm -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -e TZ=Asia/Seoul -v $(pwd):/home/jovyan/work jupyter/datascience-notebook
```

Jupyter Lab 실행 정보가 표시된 후 마지막에 접속 경로가 `http://<호스트>:8888/?token=<토큰 문자열>`과 같은 형태로 표시된다. 

해당 URL을 복사하여 Docker 컨테이너가 실행 중인 PC의 브라우저 주소창에 `http://localhost:8888/?token=<토큰 문자열>`을 입력하면 Jupyter Lab이 실행된 것을 확인할 수 있다.