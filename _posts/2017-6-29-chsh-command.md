---
layout: post
title: chsh command / awesome vim setting
---

### 디폴트 쉘을 bash로 바꾸기

```bash
chsh -s /bin/bash
```

### Automatic awesome vim setting

[https://github.com/amix/vimrc](https://github.com/amix/vimrc)

일단 위 링크에 접속하자.
readme.md를 보면 기본적인 설정과 멋진 설정을 어떻게 하는지 설명하고 있다.

멋진 설정을 위해서 다음 명령을 실행한다.

```bash
git clone https://github.com/amix/vimrc.git ~/.vim_runtime   
sh ~/.vim_runtime/install_awesome_vimrc.sh
```

쉘 스크립트를 실행하고 나면 설정이 완료되었다는 메세지가 뜨고  
vi를 이용해서 바뀐 설정을 즐길 수 있다!

![image of changed vim](https://daehankim.github.io/images/changed_vim.png)


