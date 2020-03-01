<!-- SHIELDS -->



[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]



<!-- LOGO -->



<br />
<p align="center">
  <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial">
    <img src="https://github.com/warumono-for-develop/warumono-for-develop.github.io/blob/master/logos/WARU-MONO-logo.png?raw=true" alt="Logo" width="280" height="180">
  </a>

  <h1 align="center">Spring Boot &amp; Github &amp; Docker &amp; Jenkins CI / CD Tutorial</h1>

  <p align="center">
    Spring Boot 어플리케이션을 Github 에서 관리하고 Docker 를 이용 이미지를 생성하여 Jenkins 로 자동 빌드 및 배포 처리 관련 지침서
    <br />
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial">View Tutorial</a>
    ·
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial">Report Bug</a>
    ·
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial">Request Feature</a>
  </p>
</p>



<!-- TABLE OF CONTENTS -->



## Table of Contents

* [About the Tutorial](#about-the-tutorial)
  * [Official Website](#official-website)
  * [Built With](#built-with)
* [Preview](#preview)
* [Getting Started](#getting-started)
  * [References](#references)
  * [Prerequisites](#prerequisites)
  * [Installation](#installation)
* [Usage](#usage)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [License](#license)
* [Contact](#contact)
* [Acknowledgements](#acknowledgements)



<!-- ABOUT THE PROJECT -->



## About The Tutorial

어플리케이션 배포를 자동화하여 편리하며

원격으로 배포를 진행 가능

최종적으로, 어플리케이션 + `Git` + `Docker` + `Jenkins` 를 모두 연동하여 개발에 집중할 수 있도록 하는게 목적

Jenkins 를 사용하는 이유 :
* 배포 자동화에 따른 개발에 집중 가능
* 원격 배포 가능

*Jeninks 외 다른 프로그램 또는 그 외 방법들도 있겠지만, Jenkins 프로그램을 써보는 것도 추천*

### Official Website

공식 사이트 또는 관련 정보를 미리 숙지하고 사용할 것을 권장

* [Spring Boot](https://spring.io/projects/spring-boot)

* [GitHub](https://github.com/)

* [Docker](https://www.docker.com/)

* [Jenkins](https://jenkins.io/)

* [AWS](https://aws.amazon.com/ko/)

* [Jupyter](https://jupyter.org/)

### Built with

#### Required

- [x] [Your Spring Boot Application](https://github.com/warumono-for-develop/spring-boot-restful-api-template)

- [x] [Docker Installation Tutorial](https://github.com/warumono-for-develop/docker-installation-tutorial)

- [x] [Jenkins Installation Tutorial](https://github.com/warumono-for-develop/jenkins-installation-tutorial)

- [x] [GitHub](https://github.com/)
  
- [x] [AWS](https://aws.amazon.com/ko/) EC2 Instance

  \[Free tier\] Ubuntu Server 18.04 LTS (HVM), SSD Volume Type

#### Optional

- [ ] [Jupyter Notebook Installation Tutorial](https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial)



<!-- PREVIEW -->



## Preview

**Spring Boot Application** <--- `Git` ---> **GitHub** <--- `Docker` ---> **Docker Hub** <--- `Webhook` ---> **Jenkins**



<!-- GETTING STARTED -->



## Getting Started

Spring Boot 어플리케이션의 리소스 형상 관리만으로 자동 빌드 및 배포 처리 가능하도록 처리

*본 작업을 진행에 앞서 프로그램을 설치할 대상 서버는 반드시 백업 완료 후 진행할 것을 권장*

*사용자가 사용하는 프로그램 버전과 환경 등에 따라 설명글의 진행 절차와 결과가 다소 다르거나 생략 또는 추가 작업이 있을 수 있음*

*설명글에 사용되는 용어 및 단어 등은 되도록 공식적(?)으로 사용되는 것으로 표기하였으나 오탈자 및 잘못된 용어 또는 정보가 있을 수 있음*

### References

**_`your-teminal>`_** 사용자의 터미널 프로그램 프롬프트를 나타내며 입력하는 문자가 아님

**_`{your-xxx}`_** 사용자가 정의해야하는 항목 변수이며 사용자가 직접 임의의 이름이나 특정된 값 등으로 입력

**_`{auto-xxx}`_** 사용자의 요청에 따른 결과 항목 변수이며 프로그램이 임의의 이름이나 특정된 값 등으로 노출

### Prerequisites

#### AWS EC2 인스턴스 **생성** 및 **활성화**

기존 AWS EC2 인스턴스 또는 새로운 인스턴스를 생성하여 정상적으로 구동중인 서버

#### AWS EC2 인스턴스의 **보안 그룹 설정**

AWS EC2 인스턴스에 적용되어 있는 보안 그룹으로 이동하여 Inbound 에 Jenkins 에 접속할 URL 의 PORT 추가

#### AWS EC2 인스턴스 내부 IP 정보

AWS EC2 인스턴스의 상세 정보 중 **Private IPs**

*Private IPs 정보는 터미널의 명령어를 이용하여도 확인 가능*

```sh
your-terminal> ifconfig
```

### Configuration

#### Jenkins

##### [CloudBees Docker Hub/Registry Notification 2.4.0](https://plugins.jenkins.io/dockerhub-notification/) 플러그인 설치

`Jenkins 대시보드` 화면에서 왼쪽 메뉴 중 `Manage Jenkins` 선택하여 `Manage Jenkins` 화면으로 이동

메뉴 목록 중 `Manage Plugins` 선택하여 화면 이동 후 오른쪽 상단 검색 입력 창에 `CloudBees` 입력 조회

`CloudBees Docker Hub/Registry Notification` 선택 설치 후, Jenkins 재가동

##### job Build Trigger 설정

아래 설정에 따라 Docker Hub 에서 임의의 repository 를 이미지로 만들어 등록이 완료되면 Jenkins 는 Notification 을 감지하고 **자동으로 임의의 작업 실행**

`Jenkins 대시보드` 화면에서 오른쪽 임의의 job Name 을 선택하여 Project {your-job-name} 화면으로 이동하여 왼쪽 메뉴 중 Configure 선택

Build Trigger 섹션에서 

- [ ] `GitHub hook trigger for GITScm polling` 항목 체크박스 비활성화(해제)

    *`GitHub hook trigger for GITScm polling` 은 GitHub 으로 push 되면 Jenkins 의 Webhook 에 의해 임의의 작업을 하는 것으로*

    *본 작업에서는 불필요한 작업이므로 비활성화 함*

- [x] `Monitor Docker Hub/Registry for image changes` 항목 체크박스 활성화

- [x] `Any referenced Docker image can trigger this job` 항목 체크박스 활성화

- [x] `Specified repositories will trigger this job` 항목 체크박스 활성화

`Repositories` 입력 창에 `{your-docker-image-name}` 입력

###### job Build Execute shell 설정

기존 Shell Script 가 존재한다면모두 삭제하고, 새롭게 작성

docker rm -f `{your-docker-container-name}` || true

*기존에 {your-docker-container-name} 이 구동되고 있다면 강제로 삭제*

*<strong>최초 실행(docker run)시 해당 컨테이너는 존재하지 않아 빌드가 실패</strong>하는 것을 방지하기 위하여 **_`|| true`_** 구문을 넣어 정상적으로 진행 되도록 처리*

docker pull `{your-docker-image-name}`

docker run -d -p `{your-aws-ec2-port}`:`{your-application-port}` --name `{your-docker-container-name}` `{your-docker-image-name}`

|변수|설명|예시|비고|
|---|---|---|---|
|your-docker-container-name|Docker 컨테이너 이름|spring-boot-restful-api-server-repository|Docker 실행(run) 명령어에서 지정하는 이름|
|your-docker-image-name|Docker 이미지 이름|warumono/spring-boot-restful-api-server|비고|
|your-aws-ec2-public-port|호스트 접근 PORT|8080|외부에서 접근하는 PORT 로 내부 어플리케이션 접근 PORT 와 동일하게 지정. 반드시 동일하지 않아도 무관.|
|your-application-port|어플리케이션 접근 PORT|8080|어플리케이션 개발 시 설정된 PORT|

```sh
docker rm -f spring-boot-restful-api-server-repository || true

docker pull warumono/spring-boot-restful-api-server

docker run -d -p 8080:8080 --name spring-boot-restful-api-server-repository warumono/spring-boot-restful-api-server
```

#### Docker Hub

##### Webhook 설정

`{your-docker-repository} 대시보드` 화면에서 `Webhooks 탭` 화면으로 이동

`Webhook name` 입력 창에 `{your-webhook-name}`

`Webhook URL` `http://{your-aws-ec2-public-ip}:{your-jenkins-port}/dockerhub-webhook/notify`

|변수|설명|예시|비고|
|---|---|---|---|
|your-webhook-name|Docker Hub 에서 구분하기 위한 Webhook 이름|spring-boot-restful-api-server-dockerhub|비고|
|your-aws-ec2-public-ip|AWS EC2 Public IP|54.180.113.162|비고|
|your-jenkins-port|설명|예시|비고|

```sh
spring-boot-restful-api-server-dockerhub

http://55.237.111.121:8090/dockerhub-webhook/notify
```

##### Dockerfile Build rule 설정 (Optional GitHub repository 내의 Dockerfile 을 인식 못하는 경우)

`{your-docker-repository} 대시보드` 화면에서 `Build 탭` 화면으로 이동

화면 오른쪽 위 `Configure Automated Builds` 버튼 클릭하여 `Build configurations` 화면으로 이동하여 화면 아래 부분의 `BUILD RULES` 섹션에서 `BUILD RULES` 섹션 이름 옆 `+` 버튼을 클릭하여 입력 창들이 나타남

그 중 `Build Context` 의 기본 값 `/` 즉, Dockerfile 위치가 GitHub repository 파일 구조가 프로젝트 루드 폴더로 시작하는 구조가 아닌 프로젝트 루트 폴더 내부의 파일들로 시작하는 구조인 상태의 경로가 `Build Context` 의 기본 값 `/` 을 가리킴

GitHub repository 파일 구조가 `프로젝트 루드 폴더로 시작`하는 구조

*`YourProjectFolder` 내부에 프로젝트 폴더 및 파일들이 들어 있는 경우*

**이 경우에는 `Build Context` 를 `/YourProjectFolder/` 로 입력**

```
YourProjectFolder
...
LISENSE
README.md
```

GitHub repository 파일 구조가 `프로젝트 루트 폴더 내부의 폴더 및 파일들로 시작`하는 구조

**이 경우에는 `Build Context` 기본 값 `/` 사용 또는 입력**

```
binFolder
gradle/wrapperFolder
srcFolder
.gitignore
...
Dockerfile
...
build.gradle
...
settings.gradle
LISENSE
README.md
```

GitHub repository 파일 구조가 프로젝트 루드 폴더로 시작하는 구조하고 Dockerfile 이 / 위치에 있는 경우에도 정상적으로 진행되지 않는 것으로 판단됨

인위적으로 이러한 구조를 만들어 진행하였지만 우선을 Docker Hub 에서는 인식을 못하고 빌드 자체를 진행하지 않았음

단, 그 당시 `Build Context` 의 기본 값 `/` 조차도 없었던 것으로 기억되나 좀 더 **테스트가 필요**

```
YourProjectFolder
Dockerfile
...
LISENSE
README.md
```


<!-- USAGE EXAMPLES -->



## Usage

정상적으로 모든 설정이 완료되었다면, **로컬**에서 git CLI 를 이용하여 [Spring Boot RESTFul API Server Template](https://github.com/warumono-for-develop/spring-boot-restful-api-server-template) repository 를 `clone` 하여 개발 환경 구성

Docker 명령어는 공식 사이트 또는 인터넷 등으로 미리 숙지하고 사용하는 것을 권장

타 설명글에 *[자주 사용하는 명령어](https://github.com/warumono-for-develop/docker-installation-tutorial#docker-command)* 를 간략하게 설명하였으니 참고하여 숙지하고 연습하기를 권장

#### Step 1

##### Push to GitHub

로컬에서 빌드 테스트 및 구동하여 API 테스트를 진행

테스트까지 정상적으로 완료되었다면 GitHub 으로 push

#### Step 2

##### Monitoring on Docker Hub

GitHub 의 push 를 Docker Hub 에서 감지하고 Build 진행이 되는지 Docker Hub 웹 사이트로 접속하여 확인

#### Step 3

##### Monitoring on Jenkins

Docker Hub 에서 repository 를 빌드하여 이미지로 등록 완료 처리하였음 확인

이에 따라 GitHub Notification 을 통해 Jenkins 는 감지하고 Jenkins 내부 Docker 를 이용하여 이미지를 다운로드하고 이를 구동(Docker run)

Jenkins 가 정상적으로 해당 컨테이너를 구동하였는지, 우선 터미널 또는 Jupyter Notebook 의 Terminal 로 AWS EC2 에 접근하여 도커 이미지와 컨테이너를 조회

또한, 최종적으로 웹 브라우져 또는 curl 명령어로 해당 서버 API 를 호출하여 정상적으로 결과 값을 받는지 확인

#### Step 3

##### Edit code

로컬에서 [Spring Boot RESTFul API Server Template](https://github.com/warumono-for-develop/spring-boot-restful-api-server-template) 의 코드 일부를 수정 또는 추가

*되도록 서버로부터 받는 Response 에 항목을 추가하여 기존 결과 값과 다른 것을 쉽게 파악할 수 있도록 코드 수정*

**다시 [Step 1 Push to GitHub] 부터 진행**하여 각 시스템별 정상작동 여부를 확인하고 최종적으로 수정된 사항이 반영되었는지 확인



## Roadmap

See the [open issues](https://github.com/warumono-for-develop/jenkins-installation-tutorial/issues) for a list of proposed features (and known issues).



<!-- CONTRIBUTING -->



## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project

2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)

3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)

4. Push to the Branch (`git push origin feature/AmazingFeature`)

5. Open a Pull Request



<!-- LICENSE -->



## License

Distributed under the MIT License. See [`LICENSE`][license-url] for more information.



<!-- CONTACT -->



## Contact

**warumono** - warumono.for.develop@gmail.com

Project link: [https://github.com/warumono-for-develop/jenkins-installation-tutorial](https://github.com/warumono-for-develop/jenkins-installation-tutorial)



<!-- ACKNOWLEDGEMENTS -->



## Acknowledgements

* [안경잡이개발자](https://ndb796.tistory.com/)



<!-- MARKDOWN LINKS & IMAGES -->



<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[contributors-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[forks-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/network/members
[stars-shield]: https://img.shields.io/github/stars/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[stars-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/stargazers
[issues-shield]: https://img.shields.io/github/issues/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[issues-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/issues
[license-shield]: https://img.shields.io/github/license/warumono-for-develop/jenkins-installation-tutorial.svg?style=flat-square
[license-url]: https://github.com/warumono-for-develop/jenkins-installation-tutorial/blob/master/LICENSE
[product-screenshot]: images/screenshot.png
