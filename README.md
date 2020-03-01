[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![Apache-2.0 License][license-shield]][license-url]
<!-- [![license](https://img.shields.io/github/license/:user/:repo.svg)](LICENSE) -->

<p align="center">
  <a href="https://warumono-for-develop.github.io">
    <img src="https://github.com/warumono-for-develop/warumono-for-develop.github.io/blob/master/logos/WARU-MONO-logo.png?raw=true" alt="Logo" width="260" height="160">
  </a>

  <h1 align="center">Spring Boot &amp; Github &amp; Docker &amp; Jenkins CI / CD Tutorial</h1>

  <p align="center">
    Spring Boot 어플리케이션의 리소스는 Github 에서 관리하고 Docker 로 이미지를 생성하여서 Jenkins 에 의해 자동 빌드 및 배포하는 CI/CD 작업 지침서
    <br />
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial">View Tutorial</a>
    &nbsp; <b>|</b> &nbsp;
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial">Report Bug</a>
    &nbsp; <b>|</b> &nbsp;
    <a href="https://github.com/warumono-for-develop/spring-boot-github-docker-jenkins-ci-cd-tutorial">Request Feature</a>
  </p>
</p>

## Table of Contents 목차

- [Getting Started](#getting-started)
- [Install](#install)
- [Usage](#usage)
- [API](#api)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Contact](#contact)
- [License](#license)

## Getting Started 시작하기

<kbd>⌥</kbd>    
<kbd>⌃</kbd>    
<kbd>⇧</kbd>    
<kbd>⌫</kbd>    
<kbd>⌦</kbd>    
<kbd>⌘</kbd>    

<details> 
  <summary>Collapse</summary>
  Expanded
</details>

### Requirements 요구사항

본 작업에 앞서 관련 대상 프로그램, 데이터 및 서버 등은 반드시 백업 완료 후 작업할 것을 권장   
본 작업을 작업하는 시점, 프로그램 버전 및 환경 등이 달라 설명 글의 진행 절차 또는 결과가 다소 다르거나 생략 또는 추가 작업이 있을 수 있음    
잘못된 용어 또는 정보가 다분히 포함되어 있는 비전문 지식을 바탕으로 설명되어 있으므로 공식 사이트 등에서 관련 정보를 미리 숙지하고 작업할 것을 권장

### About The Tutorial 지침서에 대하여

  - 프로그래머 입장에서의 개발이라하면 코딩뿐만이 아니라 리소스 형상관리, 빌드 및 배포작업 등은 필수적인 개발과정 중 일부   
  - 번거롭고 반복적인 작업으로 인해 효율성이 떨어지는 문제를 조금이나마 해소하고자 여러 모듈 연동   
  - 보다 나은 작업환경을 만들어 보겠다고 생소한 용어들과 이해할 수 없는 원리 그리고 설정 등으로 인해 몇 차례 포기한 경험이 있지만    
이번에야말로 완료 해보겠다는 생각으로 여러번의 실패 끝에 나름 성공한 결과를 토대로 설정 정보 및 진행순서 등을 기록한 지침서

### Prerequisites 전제조건

#### Required 필수사항

  - [x] [Spring Boot RESTFul API Server Template](https://github.com/warumono-for-develop/spring-boot-restful-api-server-template)
  - [x] [Docker Installation Tutorial](https://github.com/warumono-for-develop/docker-installation-tutorial)
  - [x] [Jenkins Installation Tutorial](https://github.com/warumono-for-develop/jenkins-installation-tutorial)

#### Optional 선택사항

  - [ ] [Jupyter Notebook Installation Tutorial](https://github.com/warumono-for-develop/jupyter-notebook-installation-tutorial)

## Install

This module depends upon a knowledge of [Markdown]().

```
```

## Usage

```
```

Note: The `license` badge image link at the top of this file should be updated with the correct `:user` and `:repo`.

### Any optional sections

## FAQ

<details> 
  <summary>User variable 사용자 변수</summary>
본 지침서는 작성자의 기준으로 설명하다보니 모든 작업의 내용대로 복사하여 사용할 경우 의도하지 않은 과정이나 결과를 도래할 수 있기에,
사용자 자신의 환경에 맞추거나 또는 원하는 내용대로 작업할 수 있도록 설명하기 위하여 변수 형태로 사용    

- `{variable-name}` 사용자가 직접 입력해야하는 부분. http://`{your-host-ip}`:8080 &nbsp; - - - > &nbsp; http://`123.456.789.0`:8080    
- `<variable-name>` 사용자의 어떠한 행위에 따른 제공되는 결과 부분. `<your-cert-key-name>`.pem &nbsp; - - - > &nbsp; `my_cert`.pem

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

## More optional sections

## Contributing

See [the contributing file](CONTRIBUTING.md)!

PRs accepted.

Small note: If editing the Readme, please conform to the [standard-readme](https://github.com/RichardLitt/standard-readme) specification.

### Any optional sections

## Contact

### Any optional sections

## License

[MIT © Richard McRichface.](../LICENSE)

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
