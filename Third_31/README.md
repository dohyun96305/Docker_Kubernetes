# Third Practice

* 여러가지 docker command 정리
                
        # for all docker command => --help shows all available config options of command
        # 왠만하면 한번씩 다시 확인해보자

        docker ps 
        # list all containers
        # -a => list all past containers including stopped containers

        docker images
        # list all images

        docker start "Docker ID or Names"
        # restart stopped container not creating new container

        # docker run : container running at foreground => attached mode (default of 'run')
        # docker run -d => start container detached mode

        # docker start : container running at background => detached mode (default of 'start')
        # docker start -a : start container attached mode

        docker attach "Container Names" 
        # detached 된 container를 attach 모드로 전환

        docker logs "Container Names"
        # detached 된 container의 log 확인 가능
        # -f => log 결과를 지속 출력

        docker run -i
        # interactive 모드 진입

        docker run -t
        # "allocate pseudo-TTY", Terminal 생성

        docker run -it "Container Names"
        # interactive 모드 및 Terminal 생성 => 상호 작용 가능

        docker start -a -i "Container Names"
        # 종료된 Container 재시작할 때 attached 모드 및 interactive 모드 진입해야함.
        # -a : attached mode 진행
        # -i : interactive mode 진행

        docker rm  "컨테이너 이름" 
        # 컨테이너 제거, 실행 중인 컨테이너는 제거할 수 없음. 

        docker run --rm "이미지 ID"
        # 이미지 기반 컨테이너 생성, 이후 중지 된 후 컨테이너는 자동으로 remove 

        docker rmi "이미지 ID"
        # 이미지 및 내부 레이어 모두 제거
        # 이미지로 생성된 컨테이너를 먼저 remove하고 이미지를 remove할 수 있다.

        docker image prune 
        # 현재 실행중인 컨테이너에서 사용되지 않는 이미지 모두 제거 

        docker image inspect "이미지 ID"
        # Image에 대해 자세한 정보를 확인할 수 있음 
        # ID, 생성 시간, 기반으로 생성된 Containers, Docker 버전, OS 

        docker cp "로컬 파일 경로" "컨테이너 이름:/"
        docker cp "컨테이너 이름:/" "로컬 파일 경로" 
        # 컨테이너 안 밖으로 파일 및 폴더를 복사할 수 있음
        # 로컬 폴더 경로/. => 경로 하위 폴더 및 파일 전부 복사
        # 컨테이너 이름:/ => 컨테이너 경로 지정
        # 실제로 실행중인 파일을 바꿀 수 없다. 
        
        # 컨테이너 내부 로그 파일을 로컬 복사로 가져와서 확인할 수 있다.

        docker run ~~~~ --name "이름 지정" 
        # 컨테이너 생성간 이름 지정 
        docker build -t name:tag 
        # 이미지에 대한 name 및 tag 지정

        docker push "이미지 이름" 
        # 이미지 공유 (pushing) => 개인 Repository로 push 가능
        # 동일한 저장소에 동일한 이미지의 여러 태그를 저장할 수 있다.

        docker pull "이미지 이름"
        # 공유된 이미지 사용 (pulling)
        # public repo에서 pull 하는데는 login 필요 X

        # docker pull => repo 내 가장 최신의 이미지를 가져옴 
        # docker run 
        # => docker run 실행간 로컬에 image가 없다면 Dockerhub에서 찾아서 최신 버전을 확인하고 가져온다.
        # 로컬에 사용한 기록이 있는 경우 최신 버전을 확인하지 않는다.

        # "이미지 이름" -> Dockerhub 
        # "HOST : 이미지 이름" => Private registry

        docker tag "이전 이름":"태크" "새로운 이름":"태그"
        # 기존 존재하는 이미지를 복제, 새로운 이름 및 태그를 가진 이미지 생성
        # 게인 레포지토리 내 push간 "도커ID/Repository name" 명령어 확인 및 이름 변경이 필요

        docker login 
        # Dockerhub 계정과 로컬과의 연결 => 개인 Reop에 push하기 위해 필요함.


- attached mode
    - Terminal과 연결된 상태 ⇒ 컨테이너의 출력 결과가 Terminal에 출력
    - docker run ⇒ attached mode가 default
    
- detached mode
    - Terminal과 분리된 상태 ⇒ 컨테이너 출력 결과가 Terminal에 출력 되지 않음
        - 컨테이너 출력 결과, 로그 메세지 등 확인되지 않음
        - 컨테이너 백그라운드 실행하면서 다른 작업을 수행할 수 있음
    - docker start ⇒ detached mode가 default

- interactive mode
    - attached, detached container내 애플리케이션과 상호 작용 (입력 등) 할 수 없다.
        - ex) 기존  container 내 .py 파일 내 int( input() ) 같은 경우 error 발생
    - interactive mode 및 Terminal 생성을 통해 애플리케이션 내 상호 작용 진행
    - 종료된 Container 재시작할 때 attached 모드 및 interactive 모드 재진입 해야함

- About Image Tags

    - name ⇒ 이미지의 여러 버전에 대한 그룹 , tags ⇒ 이미지 내 특정 버전
    - docker build -t **name:tag** ⇒ name, tag 설정 가능   


- 이미지를 기반으로 컨테이너 생성 가능 ⇒ 이미지를 주로 공유한다.
    - Dockerfile 및 Dockerfile이 속한 파일 및 코드 파일 공유
    - 완성된 이미지 파일을 공유        
        - dockerhub 혹은 private Registory로 이미지를 push 및 공유할 수 있다.
        -  Dockerhub
    
             [Docker Hub Container Image Library | App Containerization](https://hub.docker.com/)
    
        - Private Registory
          - Dockerhub 홈페이지에서 개인 Repository 생성
          - docker login 을 통해 개인 계정과 로컬에서 연결