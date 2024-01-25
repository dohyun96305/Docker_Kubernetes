# First Practice 

Docker, Container 없이 app.mjs 실행하기 위해서는 NodeJS 설치가 필요하다. <br/>
npm install 를 통해 app.mjs를 실행하기 위해 package.json 설치 

Docker Container 설정 <br/>
1. Docker Desktop 실행 여부 확인
2. Dockerfile를 통한 Image 생성 => 추후 강의때 자세한 설명 예정
3. CMD -docker build . => Dockerfile 실행 및 Image build
4. Image Build 이후 ID 확인 <br/>
   4.1 docker run -p 3000:3000 'Image ID' => -p를 통해 로컬 포트와 컨테이너 포트 연결 <br/>
   4.2 웹 - localhost:3000에서 실행 여부 확인 
5. 새로운 CMD - docker ps => 실행중인 컨테이너 확인 및 컨테이너 이름 확인
6. docker stop 'docker 이름' => 실행중인 컨테이너 종료
