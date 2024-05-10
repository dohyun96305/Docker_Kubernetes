FROM node:14
# NodeJs를 컨테이너 내부에서 이용

WORKDIR /app
# 컨테이너 내부 디렉토리 설정

COPY package.json .
# package.json을 디렉토리로 copy

RUN npm install
# npm install를 통해 package.json 설치

COPY . .
# 나머지 코드 copy

EXPOSE 3000
# app.mjs에서 설정한 port 3000 expose 

CMD [ "node", "app.mjs" ]
# node 명령을 통해 app.mjs 실행