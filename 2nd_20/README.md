# 2nd Practice - Docker Image
  
* Server.js => 기본 Node 애플리케이션 코드가 포함된 서버 JS 파일   
  * 포트 80에서 수신 대기 
* Public 폴더   
  * 스타일 지정을 위한 CSS 파일 존재
* Package.json 
  * dependencies와 Node 애플리케이션을 실행하기 위해 필요한 패키지를 포함

<br/>
** docker ps -a =>  생성된 Container 확인 가능 <br/>
** docker stop '컨테이너 이름' => 생성된 Container 확인 가능    <br/><br/>   

- local에서 실행하고자 한다면 Node JS 설치 + npm install를 통해 필요한 dependencies 설치가 필요 <br/>
- Docker에서 실행하고자 한다면 
  
      1. 이미지 빌드 및 설정을 위한 Dockerfile 생성 
          1. FROM
          2. WORKDIR
          3. COPY
          4. RUN
          5. EXPOSE
          6. CMD   
   
      2. 터미널 - docker build .
          => 경로 내 DOcker file를 기반으로 Image 생성
          => Image ID 확인

      3. 터미널 - docker run -p '로컬 포트 번호 : 컨테이너 포트 번호' '이미지 ID'
          => 이미지 기반 컨테이너 생성
          => -p : 로컬에서 애플리케이션에 엑세스하는 로컬 포트 번호 설정
          => Node 서버 실행, 

      4. 새로운 터미널 - docker ps
          => 실행중인 컨테이너 이름 확인

      5. 새로운 터미널 - docker stop '컨테이너 이름'
          => 해당 컨테이너 종료   

- 이미지 빌드 이후 코드 수정간 반영되지 않는다   
    - Dockerfile 생성 및 /app 경로로 복사 => 이후의 수정사항 반영 X
    - 코드를 삭제해도 영향 받지 않는다.
    - 코드를 변경할 때 마다 이미지를 새로 빌드해야한다..?
    - 이미지는 결국 한번 빌드된 후 "닫힌 템플릿" 
 
- 이미지는 "Layer 기반" 
    - 동일한 이미지를 다시 build할 때 빠르게 완료된다   
     => Docker는 모든 명령을 cache화 및 동일한 명령 실행간 cache된 결과를 사용
    - Dockerfile 내 모든 명령 (FROM, COPY, WORKDIR 등)을 cache화 및 Layer화
    - 수정사항, 변경된 Layer + 이후 Layer 또한 재실행
     => package.json 파일 복사 및 npm install을 선행하여 재실행 시간을 최적화 할 수 있다.     
     (npm install의 cache 결과 사용을 통해 시간 최적화)

  