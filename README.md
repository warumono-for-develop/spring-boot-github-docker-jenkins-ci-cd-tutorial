[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![Apache-2.0 License][license-shield]][license-url]
<!-- [![license](https://img.shields.io/github/license/:user/:repo.svg)](LICENSE) -->

<p align="center">
  <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial">
    <img src="https://github.com/warumono-for-develop/default/blob/master/logos/warumono-logo-492x500.png?raw=true" alt="Logo" width="292" height="300">
  </a>

  <h1 align="center">Docker Installation Tutorial</h1>

  <p align="center">
    Spring Boot & Github & Docker & Jenkins CI / CD Tutorial
    <br />
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial">View Tutorial</a>
    ·
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial/issues">Report Bug</a>
    ·
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial/issues">Request Feature</a>
  </p>
</p>



## Table of Contents 목차

- [Getting Started](#getting-started)
- [Preview](#preview)
- [Install](#install)
- [Usage](#usage)
- [FAQ](#faq)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)
- [License](#license)



## Getting Started
<!--
<details> 
  <summary>Collapse</summary>
  Expanded

---
</details>
-->

### Requirements 요구사항

본 작업에 앞서 관련 대상 프로그램, 데이터 및 서버 등은 반드시 백업 완료 후 작업할 것을 권장   
본 작업을 작업하는 시점, 프로그램 버전 및 환경 등이 달라 설명 글의 진행 절차 또는 결과가 다소 다르거나 생략 또는 추가 작업이 있을 수 있음    
잘못된 용어 또는 정보가 다분히 포함되어 있는 비전문 지식을 바탕으로 설명되어 있으므로 공식 사이트 등에서 관련 정보를 미리 숙지하고 작업할 것을 권장

### About The Tutorial 지침서에 대하여

<!--  - AWS EC2 를 사용한다면, EC2 내부의 리소스 관리는 물론 [CLI](https://namu.wiki/w/CLI) 이용 등은 필수적인 작업 중 일부   -->
  - 번거롭고 반복적인 작업으로 인해 효율성이 떨어지는 문제를 조금이나마 해소하고자 설치   
  - 보다 나은 작업환경을 만들어 보겠다고 생소한 용어들과 이해할 수 없는 원리 그리고 설정 등으로 인해 몇 차례 포기한 경험이 있지만    
이번에야말로 완료 해보겠다는 생각으로 여러번의 실패 끝에 나름 성공한 결과를 토대로 설정 정보 및 진행순서 등을 기록한 지침서

### Prerequisites 전제조건

#### Required 필수사항

  - [x] [AWS](https://aws.amazon.com/ko/) EC2 Instance    
    \[Free tier\] Ubuntu Server 18.04 LTS (HVM), SSD Volume Type

  - [x] [Spring Boot](https://spring.io/projects/spring-boot)   
    2.2.2.RELEASE   
    [Spring Boot RESTFul API Server Template](https://github.com/warumono-for-develop/spring-boot-restful-api-server-template)
    
  - [x] [Docker](https://www.docker.com/)   
    [Docker Notebook Installation Tutorial](https://github.com/warumono-for-develop/docker-installation-tutorial)
    
  - [x] [Jenkins](https://jenkins.io/)
    [Jenkins Installation Tutorial](https://github.com/warumono-for-develop/jenkins-installation-tutorial)

#### Optional 선택사항

  - [ ] [Jupyter Notebook](https://jupyter.org/)    
    [Jupyter Notebook Installation Tutorial](https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial)



## Preview

작성자가 주관적으로 이해한 내용을 토대로 간략하게 도식화한 것으로 정확한 정보는 해당 공식 사이트 등을 참조하여 이해할 것을 권장

`Spring Boot Application` <--- `git push` ---> `GitHub` <--- `connected` ---> `Docker Hub` <--- `Webhook` ---> `Jenkins`

|---------------- `사용자 작업 영역` -----------------|--------------------------- `CI / CD 작업 영역` -----------------------------|

`사용자 작업 영역` 은 일반적으로 개발 리소스 형상 관리 작업인 GitHub 으로 push 하는 행위의 영역   
`CI / CD 작업 영역` 각 모듈 별 연동 설정에 의해 빌드 및 배포 작업이 자동화 처리되는 영역    
작업의 진행 방향은 왼쪽에서 오른쪽으로 순차적으로 진행되며, 본 지침서에 의해 설정된 후에는 `사용자 작업 영역` 행위만으로 `CI / CD 작업 영역` 자동 실행 가능


## Install

### Step 1

Configure Jenkins

Install [CloudBees Docker Hub/Registry Notification 2.4.0](https://plugins.jenkins.io/dockerhub-notification/) Plugin

Docker Hub 에서 이미지 빌드 완료 후 Docker Hub 는 Notification 을 발생시키면 Jenkins 는 Webhook 로 해당 Notification 을 인식하여 임의의 작업을 진행하도록 설정하는데, 여기서 Jenkins 가 Notification 을 인식할 수 있도록 하는 Plugin

`Jenkins Dashboard` 화면 &nbsp; > &nbsp; 왼쪽 메뉴 중 `Manage Jenkins` 선택 &nbsp; > &nbsp; `Manage Plugins` 선택 &nbsp; > &nbsp; 오른쪽 상단 검색 입력 창에 `CloudBees` 키워드 입력 조회    
조회된 목록 중 `CloudBees Docker Hub/Registry Notification` 선택 설치 후, Jenkins 재가동

> CloudBees

```sh
CloudBees
```

### Step 2

Configure for connect to Github

Docker Hub 와 Github 과 연동을 위해서는 사전에 Docker Hub 사이트에서 Github 연동 설정을 완료하였거나, 새로운 Docker Hub repository 를 생성 후 Github 연동 설정을 완료하여 진행    

Docker Hub 사이트 로그인 상태에서 오른쪽 위 `<your-docker-name>` 을 선택 &nbsp; > &nbsp; 드롭다운 메뉴 중 `Account Settings` 선택 &nbsp; > &nbsp; `Account Settings` 화면 왼쪽 메뉴에서 `Linked Accounts` 선택    
`Linked Accounts` 화면에서 Provider `GitHub` 또는 `Bitbucket` 중 `GitHub` 의 `connect` 를 클릭하여 `GitHub` 계정 로그인   
정상으로 연결되면 `GitHub` 의 Account 에 <your-github-id> 가 표시됨



## Usage


[Docker](https://www.docker.com/) 사이트에 접속하여 로그인 &nbsp; > &nbsp; `Docker Dashboard` 화면 상단 `Repositories` 선택 &nbsp; > &nbsp; `Create Repository` 선택하여 새로운 repository 를 생성   

> Name {your-application-docker-image-name}

> Visibility    
>> - [x] Public

> Build Settings    
>> `Github`   
>>> Select organization {your-github-id}   
>>> Select repository {your-application-repository}

> BUILD RULES   
>> Source Type `Branch`   
>> Source `master`    
>> Docker Tag `latest`    
>> Dockerfile location `Dockerfile`   
>> Build Caching `ON`

[Spring Boot RESTFul API Server Template](https://github.com/warumono-for-develop/spring-boot-restful-api-server-template) repository 를 빌드 대상으로 지정하였고 사용자가 입력 또는 선택하는 값외에는 기본 값으로 설정

```sh
Name spring-boot-restful-api-server
Visibility
  - [x] Public
Build Settings
  Github
    Select organization warumono
    Select repository spring-boot-restful-api-server-template
BUILD RULES   
  Source Type Branch
  Source master
  Docker Tag latest
  Dockerfile location Dockerfile
  Build Caching ON
```

설정이 완료된 후, `Create` 버튼을 클릭하여 설정 저장    
*`Create & Build` 버튼을 클릭하면 설정 저장과 함께 Docerk 빌드가 진행되며 정상적으로 빌드 완료 후 Jenkins 에서도 설정에 따라 Jenkins 빌드 진행을 하는 테스트를 할 수 있음*    
*본 작업에서는 `Create` 버튼을 클릭하여 설정 저장으로 완료하고 [Usage](#usage) 에서 작업 테스트로 진행*
`<your-application-docker-repository> Dashboard` 화면으로 자동 전환되며, `Create & Build` 버튼을 클릭한 경우에는 빌드 진행 상태를 확인

### Docker 빌드 후 최종적으로 생성되는 이미지의 이름은 `{your-docker-id}/{your-application-docker-image-name}` 가 됨

> {your-docker-id}/{your-application-docker-image-name}

```sh
warumono/spring-boot-restful-api-server
```

<details> 
  <summary>Github repository 의 Dockerfile 인식 불가인 경우</summary>


`<your-application-docker-repository> Dashboard` 화면 위 Build 탭 화면 또는 `Repository never built. Click here to set up builds.` 문구의 *Click here* 를 클릭하여 화면 중간 부분 `Automated Builds` 영역에 `BUILD RULES` 정보가 나오는 것이 **정상**   
또는, Docker 빌드 진행을 하였는데 `{your-application-docker-repository} Dashboard` 화면에서 `Recent builds` 영역에 `Repository never built. Click here to set up builds.` 문구가 나오는 것은 **비정상**

먼저 프로젝트 리소스 를 Github 으로 push 하면 Github repository 첫 화면에 나타나는 두 가지의 파일 구조가 있음    
Case 1 과 Case 2 의 프로젝트는 \<your-project-folder\> 프로젝트 이름을 갖는 동일한 프로젝트

### Case 1

Github repository 파일 구조가 `프로젝트 폴더` 인 경우   
*`프로젝트 폴더` 란 작성자가 임의로 지정한 이름으로 프로젝트 생성 시 **프로젝트 이름으로 생성되는 폴더**를 말하며 이 폴더내에 소스 파일 및 폴더 등이 존재*

`프로젝트 폴더` 를 Github repository 파일 구조로 도식화

```
\<your-project-folder\>
...
LISENSE
README.md
```

### Case 2

Github repository 파일 구조가 `리소스` 인 경우   
*`리소스` 란 작성자가 임의로 지정한 이름으로 **`프로젝트 폴더` 내에 존재하는 소스 파일 및 폴더 등***

`리소스` 를 Github repository 파일 구조로 도식화

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

두 가지의 파일 구조에서 Case 1 인 경우 Docker Hub **기본 설정 값으로는 Dockerfile 을 인식하지 못하여** 빌드 진행이 되지 않음

### 원인은 Docker Hub repository 생성 시 `BUILD RULES` 의 `Build Context` 설정 부분이 잘못되어 `Dockerfile` 을 인식하지 못하는 것    
즉, Case 1 파일 구조 프로젝트 폴더 인 경우 `Dockerfile` 의 경로는 **/\<your-project-folder\>/Dockerfile** 가 되는데 기본 설정 값 (/) 에는 **/\<your-project-folder\>/** 가 빠져 있는 값이므로 정상적으로 Dockerfile 을 인식하지 못하는 결과    
그러므로, Case 2 파일 구조 리소스 인 경우 `Dockerfile` 의 경로는 **/** 가 되므로 기본 설정 값 (/) 과 정확히 맞게 되어 정상 빌드 됨    
*Build Context 항목 tip 버블 창에 설명 되어 있음*   

> Path from the repository root to the files to build. The Dockerfile location is relative to this path.

빌드 대상 프로젝트가 Github repository 에 Case 1 과 같은 프로젝트 폴더인 경우에는 Build Context 기본 값을 변경하여 설정

> Build Context /{your-project-folder}/

```sh
> BUILD RULES   
>> Source Type         Branch
>> Source              master
>> Docker Tag          latest
>> Dockerfile location Dockerfile
>> Build Context       /{your-project-folder}/
>> Build Caching       ON
```

---
</details>









### Create new Job in Jenkins

새로운 빌드 작업 (job) 생성 및 설정   
[Jenkins Installation Tutorial](https://github.com/warumono-for-develop/jenkins-installation-tutorial) 의 [Create new job](https://github.com/warumono-for-develop/jenkins-installation-tutorial/blob/master/README.md#create-new-job) 참조

> {your-jenkins-job-name}

```sh
spring-boot-restful-api-server-jenkins
```

### Configure Jenkin job Build Trigger

`Jenkins Dashboard` 화면 &nbsp; > &nbsp; 오른쪽 job 목록 중 `Name` 클릭 &nbsp; > &nbsp; `Project <your-jenkins-job-name>` 화면 &nbsp; > &nbsp; 왼쪽 메뉴 중 `Configure` 선택 &nbsp; > &nbsp; `Build Trigger` 영역

본 작업에서 `{your-application-docker-image-name}` 은 [Spring Boot RESTFul API Server Template](https://github.com/warumono-for-develop/spring-boot-restful-api-server-template) 을 Docker 이미지로 빌드하여 만들어지는 이미지의 이름으로 미리 결정하여 이 후 작업에 해당 이미지 이름을 사용하도록 함

- [ ] | \[ &nbsp;\] 체크박스 비활성화
- [x] | \[x\] 체크박스 활성화

> - [ ] GitHub hook trigger for GITScm polling    
> - [x] Monitor Docker Hub/Registry for image changes   
> - [x] Any referenced Docker image can trigger this job    
> - [x] Specified repositories will trigger this job    
> Repositories &nbsp; {your-application-docker-image-name}

```sh
[ ] GitHub hook trigger for GITScm polling
[x] Monitor Docker Hub/Registry for image changes
[x] Any referenced Docker image can trigger this job
[x] Specified repositories will trigger this job
     Repositories warumono/spring-boot-restful-api-server
```

*`GitHub hook trigger for GITScm polling` 은 사용자가 GitHub 으로 push 하면 Jenkins 의 Webhook 에 의해 이를 감지하는 기능으로, 본 지침서에서는 불필요한 작업이므로 비활성화*

### Configure Jenkin job Build Execute shell

Docker 명령어를 사용하여 이미지 다운로드, 컨테이너 삭제 및 실행 작업 등을 순차적으로 실행되도록 스크립트 작성

> docker rm -f {your-application-docker-container-name} || true   
> docker pull {your-application-docker-image-name}    
> docker run -d -p {your-host-port}:{your-application-port} --name {your-application-docker-container-name} {your-application-docker-image-name}

<details> 
  <summary><strong> || true</strong> 코드의 의미</summary>

호스트 서버 Docker 에 {your-application-docker-container-name} 의 컨테이너가 존재하지 않은 경우   
최초 본 스크립트가 실행된다면 존재하지 않는 {your-application-docker-container-name} 의 컨테이너를 삭제하는 코드 (docker rm -f) 에 의해 스크립트 에러가 발생하여 빌드 실패    
그러므로, `|| true` 코드는 오류가 있음에도 불구하고 진행이 가능하도록 처리하게 되므로 스크립트는 정상 작동

---
</details>

```sh
docker rm -f spring-boot-restful-api-server-repository || true
docker pull warumono/spring-boot-restful-api-server
docker run -d -p 8080:8080 --name spring-boot-restful-api-server-repository warumono-for-develop/spring-boot-restful-api-server
```

|변수|설명|예시|비고|
|---|---|---|---|
|your-application-docker-container-name|Docker 컨테이너 이름|spring-boot-restful-api-server-repository|Docker container 삭제 (docker rmi) 시 사용됨|
|your-application-docker-image-name|Docker 이미지 이름|warumono/spring-boot-restful-api-server||
|your-host-port|호스트 접근 PORT|8080|외부에서 접근하는 PORT 로 {your-application-port} 와 동일하게 지정. 반드시 동일하지 않아도 무관.|
|your-application-port|어플리케이션 접근 PORT|8080|어플리케이션에 설정된 PORT|


















[Preview](#preview) 의 설명과 같이 사용자는 `사용자 작업 영역` 만 진행하여 `CI / CD 작업 영역` 이 자동으로 처리된 것을 확인
정상적으로 모든 설정이 완료되었다면, 로컬 프로젝트에서 소스 일부를 편집한 후 git 명령어 또는 git 용 tool 을 사용하여 push 를 진행하고 설정에 따라 정상 동작 확인

### Edit your project source code

> edit your project soruce code as you want

[Spring Boot RESTFul API Server Template](https://github.com/warumono-for-develop/spring-boot-restful-api-server-template) 의 [RouterConfiguration.java](https://github.com/warumono-for-develop/spring-boot-restful-api-server-template/blob/master/src/main/java/com/warumono/app/configurations/RouterConfiguration.java) 파일에 일부 코드를 추가

```java
package com.warumono.app.configurations;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.HashMap;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.MediaType;
import org.springframework.web.servlet.function.RequestPredicates;
import org.springframework.web.servlet.function.RouterFunction;
import org.springframework.web.servlet.function.RouterFunctions;
import org.springframework.web.servlet.function.ServerResponse;

@Configuration
public class RouterConfiguration
{
    @Bean
    public RouterFunction<ServerResponse> ping()
    {
        return RouterFunctions.route
        (
            RequestPredicates.GET("/ping"), 
            serverRequest -> 
                ServerResponse
                    .ok()
                    .contentType(MediaType.APPLICATION_JSON)
                    .body
                    (
                        new HashMap<String, String>()
                        {
                            private static final long serialVersionUID = 1L;

                            {
                                put("ping", "pong");
                                // added new code
                                put("response", "Hello Client!");
                                put("your-param", serverRequest.param("param").orElse(null));
                                put("timestamp", LocalDateTime.now().format(DateTimeFormatter.ISO_LOCAL_DATE_TIME));
                            }
                        }
                    )
        );
    }
}
```

### Test

> curl http://{your-host-ip}:{your-host-port}/ping?param={your-parameter}

> {"ping":"pong","response":"Hello Client!","your-param":"{your-parameter}","timestamp":"{your-request-timestamp}"}

```sh
your-terminal> curl http://localhost:8080/ping?param=doesitwork
{"ping":"pong","response":"Hello Client!","your-param":"doesitwork","timestamp":"2020-03-04T23:09:05.275"}
```


## FAQ

<details>
  <summary>참조 (Reference) vs 예시 (Sample)</summary>

본 지침서는 작성자의 기준으로 설명하다보니 모든 작업의 내용대로 복사하여 사용할 경우 의도하지 않은 과정이나 결과를 도래할 수 있기에,   
사용자 자신의 환경에 맞추거나 또는 원하는 내용대로 작업할 수 있도록 설명하기 위하여 변수 형태로 사용


### 사용자 참조 내용 영역

본 지침서에 따라 작업하는 *사용자*가 아래와 같은 영역의 내용을 참조하여 **반드시 해야하는 작업**을 나열

> mkdir {your-directory-name}   
> cd {your-directory-name}    
> ls

> {your-directory-name}

> vi {your-file-name}.sh

### 작성자 예시 내용 영역

아래와 같은 영역에 *작성자*가 `사용자 참조 내용 영역`에 따라 직접 작업한 내용을 **예시**로 설명   
`사용자 참조 내용 영역` 외로 추가 작업 내용도 포함되어 설명

```sh
> cd ~
> mkdir mydir
> ls
mydir
> cd mydir
> pwd
/home/ubuntu/mydir
> sudo vi myfile.sh
```

---
</details>

<details>
  <summary>User variable 사용자 변수</summary>

본 지침서는 작성자의 기준으로 설명하다보니 모든 작업의 내용대로 복사하여 사용할 경우 의도하지 않은 과정이나 결과를 도래할 수 있기에,   
사용자 자신의 환경에 맞추거나 또는 원하는 내용대로 작업할 수 있도록 설명하기 위하여 변수 형태로 사용


- `{variable-name}` 사용자가 직접 입력해야하는 부분. http://`{your-host-ip}`:8080 &nbsp; - - - > &nbsp; http://`123.456.789.0`:8080    
- `<variable-name>` 사용자의 어떠한 행위에 따른 제공되는 결과 부분. `<your-cert-key-name>`.pem &nbsp; - - - > &nbsp; `my_cert`.pem

---
</details>

<details> 
  <summary>VIM 에디터 간단 사용 방법</summary>

본 지침서는 Linux 계열의 OS 기준으로 설명하다보니 VIM 에디터의 vi 명령어로 파일 내용을 편집하는 경우가 빈번하여 간단하게 설명   
사용자 자신의 환경과 맞지 않을 경우에는 프로그램 설치 등으로 이에 준하는 환경에서 작업할 것을 권장


### VIM 에디터 실행

vi 명령어 이용

> vi {your-file-name}

```sh
your-terminal> vi README.md
```

이 파일명의 파일이 존재하면 해당 파일을 열어서 보여주고 (아직 읽기만 가능한 상태) "{your-file-name}" file info aaa
존재하지 않을 경우 해당 파일명과 동일한 이름을 갖는 새 파일을 열음 (아직은 저장되지않은상태 ) "{your-file-name}" [New File]
이 상태에서 i또는 a또는 o를 누르면 ex 명령 부분
내용 편집 후 <kbd>esc</kbd> 를 누르면 ex 명령 모드 전환 (아직은 저장되지 않은 상태).


#### 명령 모드

**파일 내용 읽기만 가능**한 상태    
커서의 이동, 수정, 삭제, 복사, 붙여넣기 그리고 탐색 등의 기능 수행
<kbd>i</kbd>, <kbd>a</kbd>, <kbd>o</kbd>, <kbd>I</kbd>, <kbd>A</kbd>, <kbd>O</kbd> 등의 키를 눌러서 입력 모드로 전환
입력 모드 또는 ex 명령 모드 상태에서 <kbd>esc</kbd> 키를 누르면 명령 모드로 전환

|명령어 \| 키|설명|비고|
|---:|---|---|
|<kbd>i</kbd>|현재 커서 위치부터 입력||
|<kbd>I</kbd>|현재 커서 행 맨 앞에서부터 입력|<kbd>shift</kbd> + <kbd>i</kbd>|
|<kbd>a</kbd>|현재 커서 위치 다음 칸부터 입력||
|<kbd>A</kbd>|현재 커서 행 맨 끝에서부터 입력|<kbd>shift</kbd> + <kbd>a</kbd>|
|<kbd>o</kbd>|현재 커서 다음 행에 입력||
|<kbd>O</kbd>|현재 커서 이전 행에 입력|<kbd>shfit</kbd> + <kbd>o</kbd>|
|<kbd>s</kbd>|현재 커서 위치의 한 문자를 삭제하고 입력||
|<kbd>S</kbd>|현재 커서 행을 삭제하고 입력|<kbd>shift</kbd> + <kbd>s</kbd>|

#### 입력 모드 | 편집 모드 | input mode | insert mode

**파일 내용 편집이 가능**한 상태    
명령 모드에서 입력 전환키를 누르면 에디터의 왼쪽 아래 모서리 부분에 `-- INSERT --` 로 전환되었음을 알려주고 <kbd>esc</kbd> 키를 누르면 `-- INSERT --` 가 사라지므로써 입력 모드에서 명령 모드로 전환됨
자주 사용되는 명령어는 다음 표와 같으며 대부분 화면에 입력한 키가 나타나지는 않으므로 현재 모드를 확인하며 작업

|명령어 \| 키|설명|비고|
|---:|---|---|
|<kbd>x</kbd>|현재 커서가 위치한 문자 삭제|<kbd>del</kbd>|
|<kbd>dw</kbd>|단어 삭제||
|<kbd>dd</kbd>|현재 커서가 위차한 행 삭제||
|{숫자} + <kbd>dd</kbd>|현재 커서가 위치한 행부터 숫자만큼의 행 삭제||
|<kbd>yy</kbd>|현재 커서가 위치한 행 복사||
|{숫자} + <kbd>yy</kbd>|현재 커서가 위치한 행부터 숫자만큼의 행 복사||
|<kbd>p</kbd>|복사한 내용을 현재 커서가 위치한 행 이후 행에 붙여 넣기||
|<kbd>P</kbd>|복사한 내용을 현재 커서가 위치한 행 이전 행에 붙여 넣기|<kbd>shift</kbd> + <kbd>p</kbd>|
|<kbd>u</kbd>|직전 실행한 명령 취소|undo|
|<kbd>/exp</kbd> + <kbd>enter</kbd>|'exp' 문자열을 현재 커서 위치에서 오른쪽 또는 아래 방향에서 검색||
|<kbd>n</kbd>|찾은 문자가 여러개인 경우 현재 커서 위치에서 오른쪽 또는 아래 방향으로 일치하는 다음 문자 위치로 이동||
|<kbd>N</kbd>|찾은 문자가 여러개인 경우 현재 커서 위치에서 왼쪽 또는 위 방향으로 일치하는 이전 문자 위치로 이동|<kbd>shift</kbd> + <kbd>n</kbd>|

### ex 명령 모드 | 라인 명령 모드
명령 모드 상태에서 입력하는 키가 `에디터의 왼쪽 아래 모서리 부분`에 나타나며 ex 명령어를 이용하여 **에디터 저장, 종료, 탐색, 치환 및 vi 환경 설정 등이 가능**한 상태
명령 모드에서 <kbd>:</kbd> 키 입력으로 시작

|명령어 \| 키|설명|비고|
|---:|---|---|
|<kbd>q</kbd>|편집기 종료||
|<kbd>w</kbd>|저장||
|<kbd>!</kbd>|강제실행||

```
:q
```
편집한 내용이 없는 경우, 편집기 종료   
편집한 내용이 있는 경우, 저장하지 않았다는 에러 메시지를 보여주며 편집기는 종료되지 않음


```
:q!
```
내용을 편집하였든 하지 않았든 저장하지 않고 편집기 종료


```
:wq
```
편집한 내용은 저장하고 편집기 종료


### VIM 에디터 줄 번호 보기

지정된 파일 이름으로 생성하여 명령어 한 줄 입력 후 저장하는 것만으로 설정 가능

> vi ~/.vimrc

```sh
your-terminal> vi ~/.vimrc
```

.vimrc 파일에 명령어 한 줄 입력 후 저장

> set number

```sh
set number
```
* 또한, 파일 내용 보기 명령어 `cat` 은 옵션 `-n` 을 이용하여 줄 번호 보기 가능

> cat -n {your-file-name}

```sh
your-terminal> cat -n .vimrc
     1  set number
```

### sudo | su | su -

|명령어|설명|비고|
|----|---|---|
|sudo|다른 계정의 권한만 빌림|슈퍼유저 보안권한으로 프로그램을 구동할 수 있음. 기본 값 슈퍼유저.|
|su|다른 계정으로 전환|로그아웃을 하지 않고 다른 사용자 계정으로 전환|
|su -|다른계정으로 전환|다른 사용자 계정으로 전환하고 변경된 계정의 환경변수 이용|

---
</details>

<details> 
  <summary>Docker 명령어 간단 사용 방법</summary>

[Use the Docker command line](https://docs.docker.com/engine/reference/commandline/cli/)

모든 명령어의 뒤에 `--help` 를 입력하면 해당 명령어의 사용법이 표기 됨

> docker images --help

```sh
your-terminal> docker images --help
```

#### About image

* Docker Hub 로 부터 이미지 조회

> docker search {your-docker-image-search-keyword}

```sh
your-terminal> docker search hello
```

* 이미지 목록 조회

> docker images

```sh
your-terminal> docker images
```

* Docker Hub 로 부터 이미지 다운로드

> docker pull {your-docker-image-name}:{your-docker-image-tag}

```sh
your-terminal> docker pull hello-world:latest
your-terminal> docker pull hello-world:0.1.9
```

* 이미지 삭제

> docker rmi {your-docker-image-id}

```sh
your-terminal> docker rmi 1f1b68f35fa5
```

* 이미지 전체 삭제

> docker rmi \`docker images\`

```sh
your-terminal> docker rmi \`docker images\`
```

### About container

* 컨테이너 목록 조회

> docker ps \[-a\]

|옵션|설명|형식|예시|
|---|---|---|---|
|-a|중지되었거나 구동중인 모든 컨테이너 포함||-a|

```sh
your-terminal> docker ps
your-terminal> docker ps -a
```

* 컨테이너 실행

> docker run [options] image[:TAG|@DIGEST] [COMMAND] [ARG...]

\[options\]

|옵션|설명|형식|예시|
|---|---|---|---|
|-d|detached mode. 백그라운드 모드||-d|
|-p|port. 호스트와 컨테이너의 포트를 연결 (포워딩)|호스트 포트:컨테이너 포트| -p 9090:8080 |
|-v|volume. 호스트와 컨테이너의 디렉토리를 연결 (마운트)|호스트 디렉토리 경로:컨테이너 디렉토리 경로|-v /your/dir/path:/var/www/http|
|-e|enviroment. 컨테이너 내에서 사용할 환경변수 설정|...|...|
|--name|컨테이너 이름 설정|컨테이너 이름|a-container thecontainer|
|--it|컨테이너의 표준 입력과 로컬 컴퓨터의 키보드 입력을 연결||-it|
|--rm|remove. 프로세스 종료시 컨테이너 자동 제거|컨테이너 ID|--rm 1f1b68f35fa5|
|--link|컨테이너 연결|컨테이너 이름:별칭|a-container:mycontainer|

```sh
your-terminal> docker run --rm -d -p 9090:8080 hello-api --name api
```

* 컨테이너 시작

> docker start {your-docker-container-id-or-name}

```sh
your-terminal> docker start 1f1b68f35fa5
your-terminal> docker start hello-world
```

* 컨테이너 재시작

> docker restart {your-docker-container-id-or-name}

```sh
your-terminal> docker restart 1f1b68f35fa5
your-terminal> docker restart hello-world
```

* 컨테이너 접속

> docker attach {your-docker-container-id-or-name}

```sh
your-terminal> docker attach 1f1b68f35fa5
your-terminal> docker attach hello-world
```

* 컨테이너 중지

> docker stop {your-docker-container-id-or-name}

```sh
your-terminal> docker stop 1f1b68f35fa5
your-terminal> docker stop hello-world
```

이 외, <kbd>e</kbd><kbd>x</kbd><kbd>i</kbd><kbd>t</kbd> 을 입력하거나,   
<kbd>control</kbd> + <kbd>D</kbd> 를 누르면 컨테이너 중지

<kbd>control</kbd> + <kbd>P</kbd> -----> <kbd>control</kbd> + <kbd>Q</kbd> 를 순서대로 누르면 컨테이너를 중지시키지 않고 나옴

* sudo 명령어 없이 Docker 명령어 사용할 수 있는 팁

Case 1    
현재 접속중인 사용자에게 sudo 권한 부여

```sh
your-terminal> sudo usermod -aG docker $USER
```

Case 2    
임의의 사용자에게 sudo 권한 부여

```sh
your-terminal> sudo usermod -aG docker {your-user-name}
```

---
</details>



## Contact

**email** warumono.for.develop@gmail.com    
**blog** https://warumono-for-develop.github.io

## Acknowledgements

* [안경잡이개발자](https://ndb796.tistory.com/)

## License

Distributed under the MIT License. See [`LICENSE`][license-url] for more information.

<!-- MARKDOWN LINKS & IMAGES -->

<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

[spring-boot-restful-api-server-template]: https://github.com/warumono-for-develop/spring-boot-restful-api-server-template "Spring Boot RESTFul API Server Template"
[spring-boot-github-docker-jenkins-ci-cd-tutorial]: https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial "Docker Installation Tutorial"
[spring-boot-github-docker-jenkins-ci-cd-tutorial]: https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial "Jenkins Installation Tutorial"
[spring-boot-github-docker-jenkins-ci-cd-tutorial]: https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial "Jupyter Notebook Installation Tutorial"

[contributors-shield]: https://img.shields.io/github/contributors/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial.svg?style=flat-square
[contributors-url]: https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial.svg?style=flat-square
[forks-url]: https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial/network/members
[stars-shield]: https://img.shields.io/github/stars/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial.svg?style=flat-square
[stars-url]: https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial/stargazers
[issues-shield]: https://img.shields.io/github/issues/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial.svg?style=flat-square
[issues-url]: https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial/issues
[license-shield]: https://img.shields.io/github/license/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial.svg?style=flat-square
[license-url]: https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial/blob/master/LICENSE
[product-screenshot]: images/screenshot.png
