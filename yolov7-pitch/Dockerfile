FROM python:3.8.3

ENV APP_ROOT /src
ENV CONFIG_ROOT /CONFIG_ROOT

RUN apt-get update
# RUN apt-get install ffmpeg libsm6 libxext6 -y
RUN apt-get install -y zip htop screen libgl1-mesa-glx

RUN mkdir ${CONFIG_ROOT}
COPY requirements.txt ${CONFIG_ROOT}/requirements.txt
RUN pip install -r ${CONFIG_ROOT}/requirements.txt

RUN mkdir ${APP_ROOT}
WORKDIR ${APP_ROOT}
ADD .  ${APP_ROOT}