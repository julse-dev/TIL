# WSL2 세팅해보기

#### 작성일: 2025-04-30 16:18

### WSL2을 왜 설치해보려고 하는가?

> MacOS와 Linux에서는 Terminal을 통해 개발환경을 구축하고 여러 작업을 편하게 할 수 있습니다.</br> Windows도 PowerShell이나 Windows Terminal, CMD 등을 사용해서 개발환경을 구축할 순 있으나.. 다른 OS에 비해서는 약하다는 느낌이 들었습니다. 또한 Mac의 Homebrew나 Ubuntu의 apt와 같은 환경을 갖추고 싶다..라는 마음이 커졌습니다. </br> 참고로 Chocolatey라는 Windows진영의 package manager가 있긴 하지만 이 역시 다른 OS에 비해 약하다는 것을 느꼈고, 그렇다면 WSL2를 사용해서 개발환경을 구축하면 어떨까 궁금했기에 집에서 사용하는 Windows PC에 셋업을 해봤습니다... 만 아직 엄청난 Power라던가 그런 것은 느끼지 못했기에 일단 과정을 기록해봅니다.

### WSL2 세팅

1. Windows 공식문서 확인하기

   > 바로 PowerShell이나 CMD를 켜서 커맨드를 입력할 수 없습니다. 우리는 지식이 필요합니다. </br> 마이크로소프트의 공식문서는 세팅하는 방법에 대해 한국말로 하나하나 알려주니 꼭 참고해봅니다.
   >
   > > [Windows WSL 공식문서](https://learn.microsoft.com/ko-kr/windows/wsl/)

2. 필수 조건 확인하기

   > WSL을 사용하기 위해서는 반드시 확인해야할 사항이 있다고 합니다. </br> "Windows 10 버전 2004 이상(빌드 19041 이상) 또는 Windows 11을 실행해야 합니다." </br> 제 OS는 이미 Windows 11이기에 조건에 부합합니다.
   >
   > > [WSL을 사용하여 Windows에 Linux를 설치하는 방법](https://learn.microsoft.com/ko-kr/windows/wsl/install)

3. 터미널 열고 커맨드 입력

   > 필수 조건도 확인했으니, PowerShell이든 CMD이던 <b>관리자모드</b>로 실행하고 커맨드를 입력합니다.
   >
   > > `wsl --install` </br></br> 참고로, 기존에 wsl이 전혀 설치되어있지 않은 상태여야 한다고 합니다. 주의사항은 꼭 읽어줍시다!

4. Linux 목록보고 설치하기

   > 설치할 Linux의 목록을 확인하고 Linux를 설치해봅시다. </br> 설치 가능한 목록을 확인해보니 Ubuntu가 24.04 lts가 나왔길래 설치했었는데, 친구 말로 아직은 버그가 많다고 20번대가 낫다고 합니다. ㅎㅎㅎ;
   >
   > > `wsl --list --online` >> `wsl.exe --install <설치할 Linux>`

5. 개발환경 구성하기

   > WSL 설치를 완료하면, 사용자의 입맛에 맞게 개발환경을 구성하면 됩니다! </br> 이 역시 마소가 공식문서를 잘 해놨기에 첨부해놓고...
   >
   > > [WSL 개발 환경 설정](https://learn.microsoft.com/ko-kr/windows/wsl/setup/environment)

6. Node.js 및 Postgresql 설치하기 <br> !!! 여기서부터는 개인적으로 구성한 환경입니다. <br> !!! 사용해보면서 추가하거나 보완할 점이 있으니 참고용으로만 보시길 바랍니다.

   > > 자세한 것은 공식문서를 참고합시다 >> [WSL에서 Node.js 설치하기](https://learn.microsoft.com/ko-kr/windows/dev-environment/javascript/nodejs-on-wsl)
   >
   > 1. cURL(명령줄에서 인터넷에서 콘텐츠를 다운로드하는 데 사용되는 도구) 설치 <br> `sudo apt-get install curl`
   >
   > 2. nvm 설치 <br> `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash`
   >
   > 3. Node.js LTS 릴리스 설치 <br> `nvm install --lts`
   >
   > 4. 설치된 Node 버전 및 npm 버전 확인 <br> `node --version` && `npm --version`
   >
   > 5. VSCode와 연결하기 <br> [1. Windows 로컬에서 VSCode 설치](https://code.visualstudio.com/) <br> [2. VSCode에서 Remote-WSL 익스텐션 설치](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)
   >
   > 6. WSL에서 프로젝트 열어보기 <br> 1. WSL에서 프로젝트 경로로 이동 <br> 2. `code .`
   >
   > 여기까지가 WSL에서의 Node.js 세팅 과정이었습니다. 큰 문제가 없다면 WSL환경의 프로젝트가 VSCode에서 실행될 것입니다.
   >
   > > Postgresql도 공식문서가 잘 되어있습니다. >> [WSL에서 Postgresql 설치하기](https://learn.microsoft.com/ko-kr/windows/wsl/tutorials/wsl-database#install-postgresql)
   >
   > 1. Ubuntu 패키지 업데이트 <br> `sudo apt update`
   >
   > 2. Postgresql(및 유용한 유틸리티가 있는 -contrib 패키지) 설치 <br> `sudo apt install postgresql postgresql-contrib`
   >
   > 3. 버전 확인 <br> `psql --version`
   >
   > 4. postgresql 세팅하기.. 여기부터는 공식문서를 확인해주세요.

7. Github에서 프로젝트 가져오기
   > 1. 프로젝트를 가져오는 방법은 구글에 검색만 해도 잘 찾아볼 수 있습니다. <br> 다만 github 계정과 관련된 토큰 관련 이슈는 조금 검색이 필요했는데, 이를 위해 도움받은 [블로그 주소(이령님의 블로그)](https://s-ryung.tistory.com/54)를 남깁니다.
   >
   > 2. 제 개인 프로젝트는 npm으로 관리하는 Nest.js 프로젝트와 yarn으로 Next.js 프로젝트가 있었는데, yarn이 Ubuntu에서는 설치할 때 확인해야 할 점이 있었습니다. <br> 이 역시 도움받은 [블로그 주소(SdardewValley님의 블로그)](https://sdardew-valley.tistory.com/69)를 남깁니다.

### 그래서 이제 뭐함?

> 사실 개발환경을 뭔가 어마무시한 마음을 먹고 WSL로 엎자! 했던 것인데, 설치했던 Ubuntu 24.04를 밀고 20.04로로 새로 설치해야하는 귀찮음이.. 있습니다. <br> 그래도 Windows에서 WSL을 통해 개발할 일이 생기면 이렇게 미리 시도를 해봤기에 다음 경우에는 시행착오를 덜 할 것 같다..고 생각됩니다. <br> 또한 개인적으로 기록을 남기는 것을 잘 못하는 편인데, 이번 포스팅을 통해 하나하나 작성할 수 있으면 좋겠습니다.
