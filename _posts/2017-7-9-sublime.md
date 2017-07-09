---
layout: post
title: Ubuntu Sublime Text 3 Settings
---

### Sublime text

Sublime Text는 Jon Skinner가 개발한 텍스트 에디터입니다. 가벼운 크기와 심플한 디자인, python을 이용한 다양한 플러그인 확장이 가능한 장점으로 많은 개발자들이 애용하고 있습니다. 

![sublime text](http://canorus.github.io/Resources/2016-08-10/showconsole.png)

-------

### Font, Word-wrap setting

먼저 sublime text를 설치한 디렉토리에 packages를 찾습니다. packages 안에 Default.sublime-package라는 .zip파일의 압축을 풀어줍니다. 저는 default라는 이름의 폴더를 만들어서 그 내부에 풀어줬습니다. 밖에 풀면 골치 아파요.  

그리고 Preferences(Lunux).sublime-settings라는 파일을 열어줍니다. 내부는 이렇게 생겼을 거예요.

```javascript
{
	"font_face": "Monospace",
	"font_size": 10,
    "mouse_wheel_switches_tabs": true,
}
```

여기에서 원하는 폰트와 사이즈로 바꿔주고, 자동 줄바꿈을 위해서 다음 설정을 추가해줍니다.  

```javascript
{
	"font_face": "Monaco",
	"font_size": 24,
    "mouse_wheel_switches_tabs": true,
    "word_wrap": true
}
```

이렇게 한 후에 default 폴더에 있던 모든 파일을 모아 압축해줍니다.

```bash
zip Default.sublime-package ./*
```

그리고 원래 있던 Default.sublime-package 파일과 새로 만들어진 파일을 바꿔주고 sublime text를 실행해보세요. 바뀐 화면을 확인하실 수 있습니다.

 ![changed sublime](https://daehankim.github.io/images/new_sublime.png)

-------

### 한글 입력 문제 

Sublime Text 3는 아쉽게도 한글 입력을 지원하지 않습니다. 하지만 한 중국 개발자가 만든 스크립트 덕분에 완벽하지는 않지만 나름 쓸만하게 한글을 입력할 수 있습니다.

다음 명령어로 깃 저장소를 받아오고 필수 패키지를 설치해 줍니다.

```bash
git clone https://github.com/lyfeyaj/sublime-text-imfix.git
sudo apt-get install build-essential libgtk2.0-dev
```

그리고 src에 들어가 .c파일을 컴파일 해줍니다.
```bash
cd sublime-text-imfix/src/
gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
```

이제 libsumlime-imfix.so 파일이 생겼을 겁니다. 한글을 쓰려면 libsublime-imfix.so를 먼저 로딩한 후에 sublime text 3를 실행시켜야 합니다. 먼저 생성된 파일을 /opt/sublime_text/lib로 옮겨주고 나서 간단한 쉘 스크립트를 짜 봅시다.

```bash
sudo mkdir /opt/sublime_text/lib
sudo mv ./libsublime-imfix.so /opt/sublime_text/lib/
```

*launch_sublime*  
```bash
#!/bin/bash
export LD_PRELOAD=/opt/sublime_text/lib/libsublime-imfix.so
exec /opt/sublime_text/sublime_text "$@"
```

만들어진 launch_sublime 파일을 opt/sublime_text로 옮겨줍니다.

```bash
sudo mv ./launch_sublime /opt/sublime_text/
```

이제 마지막으로 .bashrc를 수정해줘야 하는데요. 파일을 연 후 다음 부분을 추가해주세요.

```bash
alias sub=/opt/sublime_text/launch_sublime
```

그리고 바뀐 배쉬 설정파일을 적용하기 위해 다음을 실행해 줍니다.

```bash
source ~/.bashrc
```
그러면 이제 command line에서 sub 명령어로 sublime-text 3를 즐길 수 있습니다!

![sublime text 한글](https://daehankim.github.io/images/subhangul.png)
