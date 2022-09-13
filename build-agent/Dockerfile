FROM node:latest


RUN apt-get update
RUN apt-get install -y git


RUN git clone https://github.com/ArturHamerski98/react-tetris.git
WORKDIR react-tetris


RUN npm install
RUN npm run build
