--
layout: post
title:  "Windows 에서 Git server 설치"
date:   2018-08-11 18:56:00 +0900
categories: [Multimedia and Programming, Jekyll_and_others]
tags:
  - Git
  - Windows 
comments: true
---

* Table of Contents
{:toc}

## HTTP 서버를 기반으로 한 Git Server 설치

많은 사람들이 가정에서 사용하는 PC는 거의 대부분 Windows일 것이라 생각한다. 아무래도 WIndows OS가 범용적이기 떄문이니까. 그리고 많은 개발자들이 버전 관리가 잘 되는 어떤 솔루션을 원하는 것도 사실이다. 대표적으로 Subversion과 Git이 될 것이다.
특히 Git을 운용하는 사람들의 경우, 많은 경우, Github 혹은 유사한 클라우드 기반 Git Service를 사용하고 있다.
물론 대부분은 공짜로 사용하고 있다. 덕택에, 그런 경우는 Repository의 제한이나, 혹은,  코드를 모두 공개하고 사용할 수 밖에 없을 것이다.
하지만, 작은 프로젝트라도 협업을 해야하는, 혹은 공개가 되어서는 안되는 경우라면, 얘기가 달라진다. 어쨌든 공개가 되어서는 안되니까. 따라서, 이런 경우, 나만의 Git Server를 운용하였으면 하는 생각을 하게 된다. 그것도 어떠한 제한도 없이..

Linux의 경우에는 솔루션이 거의 널려 있다고 봐도 과언이 아니다. 
하지만, Windows의 경우는 얘기가 다르다. 

이러한 경우, 완전히 Open Source Solution만 가지고 Windows에서 Git Server를 운용할 수 없을까? 하는 생각을 하게 될 것이다.

간단한 경우, 방법이 있다. 그것은 WIndows용 HTTP 서버를 설치하고, Git 서버도 설치한 후, HTTP 서버의 Config 파일만 수정하면 된다.
물론, Git Server 자체가 사용자 인증을 필요로 하기 때문에 HTTP 서버에서 제공하는 사용자 인증 서비스를 Git Server에 연결해 주는
과정이 필요하다.

이러한 방법 중 가장 간단한 방법은 HTTP 서버의 WebDaV를 사용하여 Git 서버의 사용자 인증을 대신하는 방법이다.
물론 Open SSL 서버를 사용하여 인증을 하는 방법도 생각할 수 있을 것이나, 상대적으로 HTTP 서버 기반으로 Git 서버 서비스를 운용하는 것이 쉽다.

만일, Git Server 단독으로는 안되느냐고 생각할 수 있겠지만, 안된다.

Subversion도 마찬가지지만, HTTP 프로토콜을 기반으로 버전 관리 서버들이 대체로 운용되기 때문이다.

따라서, 앞에서 언급한 대로 Windows의 HTTP 서버를 기반으로 Git 서비스를 구현하는 방법을 논하고자 한다.
개인적으로는 이 방법이 그 어떤 방법보다 가장 쉬운 방법이라 생각한다.

## Redmine Apache 서버를 사용한  Git Server 설치
  
Windows에 HTTP 서버 서비스를 구현하는 가장 간단한 방법은 **Bitnami**에서 제공하는 Apache 서버 솔루션을 설치하고 그 위에서 Git 서버를 구현하는 것이다. ([Bitnami App Catalog Link](https://bitnami.com/stacks))  혹은, 아예 Apache Home Page에서 Windows용 Apache를 설치하고 (디렉토리 구조가 동일하다) Git Server를 설치한 후, Apache 서버의 Config을 조절하여 구현할 수 있다. 

대체로 Bitnami에서 제공하는 Apache 서버의 경우 설치 디렉토리만 잘 세팅되면 나머지 디렉토리 구조는 기본의 WIndows용 Apache 서버와 같은 디렉토리 구조를 가진다. (이점은, Redmine의 경우 버전이 달라지면 Ruby 관련 디렉토리가 달라지는 것과 비교하여 좋은 점이라 볼 수 있다.)

Windows에서 제공하는 HTTP 서버 기능인 IIS 의 경우에는, 기존의 Apache 서버와 디렉토리 및 Config이 다른 점이 있기에 쉽게 Reference를 얻기가 어려운 단점이 있다. 그 외, 몇가지 Linux에서의 Git 서비스 설치와 Windows에서의 Git Service 설치에 차이점이 있다. 

일낟, 많은 경우, Windows의 Apache 서버 세팅 대신 Linux Apache 서버 세팅인 관계로 Windows에서 어떻게 Git 서버 세팅이 가능한지, 잘 나와 있지 않은 경우가 많다..  그러나 생각보다 쉽다.

Windows에서 Apache를 "C:\Apache"로 설치하였다고 가정하자.
그러면 이후 디렉토리는 여기에 있다고 보고 주로 Check해야 하는 것은 **"C:\Apache\htdocs" 디렉토리가 된다.**

편의상, 이후에는 "./htdocs" 디렉토리라고 하면  **"C:\Apache\htdocs"** 라 생각하면 된다.

### Git 서비스를 위한 디렉토리 설정

**현재, Apache 서버와 Windows 용 Git이 모두 설치 되어 있다고 가정하자.**

먼저 서버의 경우 다음과 같이 bare Git Repository를 **htdocs** 디렉토리에 만든다.

이 두 명령어는 Windows Commander로 만들거나 Command 창에서 당음과 같이 DOS 명령어를 직접 입력해서 만든다.

~~~
mkdir test_git.git
cd test_git.git
~~~
 
git 명령은 Windows용 Git Bash를 사용해야 한다. 디렉토리는 **test_git.git** 이다. (즉, c:\apache\htdocs\test_git.git)

~~~
git --bare init
git update-server-info
~~~

즉, Command 창과 Git Bash 창을 동시에 사용해야 한다.
다음 WebDav를 활성화 시켜야 한다. 

 
### Apache WebDav 활성화


Apache 서버에서 **httpd.conf** 파일을 찾는다. 작업을 위해 일단, bakup을 하나 만들어 놓자.     
다음 httpd.conf 파일을 수정하여 에서 WebDav 활성화 시킨다.

일단, Apache 서버를 끄고 (현재 디렉토리는 c:\apache 라 가정하자.)

**/conf/httpd.conf** 에서 다음을 찾아보자.
~~~
Dynamic Shared Object (DSO) Support
~~~
 
이 항목에서 다음의 Module 3개가 모두 Load 되도록 한다.

~~~
LoadModule dav_module modules/mod_dav.so
LoadModule dav_fs_module modules/mod_dav_fs.so
LoadModule dav_lock_module modules/mod_dav_lock.so
~~~

현재 httpd.conf 에

~~~
DocumentRoot "C:/apache2/htdocs"
~~~
로 설정되어 있을 것이다. (Windows용 Apache 서버를 설치하면 그렇게 되어 잇는 경우가 많다. 만일 다른 Service 예를 들어 Redmine에서 사용하는 Apache서버라면 다음과 같을 것이다. "C:\Bitnami\Redmine-3-3-2\apache2\htdocs") 해당 Root의 형식이 그 밑에 설정되어 있다.

나중에 환경변수로 Git Repository 를 설정하고 비슷하게 만들어서 실험해 보자.


그 다음 Password File을 생성해야 한다. Bin 밑에 보면 htpasswd 가 있다. 이것을 사용하여 다음과 같이 만들자.
(현재, ./conf 디렉토리로 가정하자.) 
~~~
$ htpasswd -c passwd.git <user>
~~~

만일 htpasswd.exe 가 불려지지 않는다면 이는 PATH 문제이다. ./bin 디렉토리 밑에 htpasswd.exe 가 존재하니, 거기서 똑같이 해주면 된다. 

그러면 password 를 묻는다. Password를 입력하면 passwd.git 파일이 생성된다.

passwd.git 파일을 /conf 밑에 복사한다.

사용자를 추가하기 위해서는 위에서 passwd.git 에 –c 옵션 없이 사용자를 추가하면 된다.

다시, httpd.conf 파일을 열어서 다음과 같이 편집한다.

~~~
# WebDAV for Git Server
# First Locking DAV Operation using DavLockDB
# Second Including the following Directory
#

DavLockDB  "c:\apache\var\DavLock"

<Location /test_git.git>
     DAV on
     AuthType Basic
     AuthName Git
     AuthUserFile conf/passwd.git
     Require valid-user
</Location>
~~~
 

주의할 점은 DavLockDB 경로를 잘 적어 주어야 한다는 점이다. (존재하지 않는다면 아무 Editor를 열고 해당 파일을 그냥 만들어 준다. 그러면 0 바이트의 DavLockDB 파일이 만들어진다. 단, 자동으로 만들어지는 것은 아니고 Apache 서버를 다시 가동 시켰을 때 만들어지는 것이므로 기동시킨 후 해당 파일이 생성되는지 살펴봐야 한다.)

User의 경우 **valid-user**로 해주어야 한다.

Apache 서버를 다시 Enable 시킨다.

이 정도만 하면

http://jnwhome.iptime.org/test_git.git 하면 해당 페이지를 볼 수 있다 (웹 브라우저에서 ID와 PW 를 묻게 되니 이를 입력 한 후 볼 수 있다)

여기까지 하면, Http 서버에서 WebDAV를 사용하여 Git Server와의 연동이 끝난다.
즉, HTTP 서버는 WebDAV 서비스를 Git Repository 디렉토리에 연결시키는 것이고
Git은 Git Bare Repository에 있는 정보를 사용하여 Git Server Service를 시작하는 것이다.

### 아직, 끝이 아니다. 

그리고 가장 중요한 점은…

**Test_git.git 폴더의 권한**을 잡아 주어야 한다. Linux에서는 이 부분을 chmod 혹은 chown -R www.www 을 통해 수행하는데 Windows 에서는 전혀 다르다. Windows에서는 Exploere 에서 git Repository인 test_git.git 에 우측 마우스를 대고 **속성->보안**으로 들어가서

**Authenticated Users**를 **모든 권한**으로 해 주어야 한다. 안 그러면 Git 에서 에러가 난다. 이로서 **WebDav로 인증된 사용자가 Git Remote 서버를 인증하여 사용**할 수 있게 된다.
 

## Client 에서 Git Server 동작 테스트

### Git Bash 에서의 테스트
만일 Git Bash가 있다면 다음과 같이 하여 Git Server 테스트 겸 README 파일을 Commit 시키게 된다. (경로는 Windows 경로가 되도록 한다)
 
~~~
mkdir ~/Desktop/test-project
cd ~/Desktop/test-project
git init
git remote add origin http://<user>@<server name or IP address>/test-project.git
touch README
git add .
git commit -a -m “Initial import”
git push origin master
~~~
 
### TortoiseGit 에서의 테스트
만일 TortoiseGit 이 설치되어 있다면 다음과 같이 한다.

일단, Git Repository here 를 수행하여 특정 폴더를 git Repository 로 만든다. (당연하지만, Bare로 만들면 안된다. Bare는 서버 Side의 Repository이다.)

**TortoiseGit -> Setting -> Git** 에서 설정을 확인한 후 (사용자 정보와 이메일)

**Git->Remote**를 설정한다. (매우 중요)

~~~
<URL>
http://jnwhome.iptime.org/test_git.git
~~~
 
이것만 넣어 주어도 자동적으로 origin 이 뜬다. 다음이 중요하다.

~~~
<Push URL>
http://MyID:MyPW@jnwhome.iptime.org/test_git.git
~~~
 
**꼭 ID와 PW를 http:// 앞에 같이 써주어야 한다.**

그리고 PUSH를 해주면 Remote에 Push가 된다.

### 주의할 점 

가급적 Git의 버전을ㅇ 2.10 이상의 것으로 하기 바란다.
최근 Git 이 1.x대 버전에서 2.x 버전으로 업그레이드 하면서 Git 자체의 특성이 변화되어 제대로 Push/Pull이 안되는 에러가 발생한다.
이를 해결하는 것은 결국 Git 자체를 업그레이드 하는 것 외에 방법이 없다 (Server 및 Client 모두)

그러므로, 본 페이지에 나와 있는 Git 서버 설치를 하기 전에 Git의 업그레이드를 Server 및 Client 모두에서 먼저 수행하기를 바란다.


## Reference

본 내용과 관련하여 기본적인 사항은 다음 사이트를 참조한다.

[1] [Git --local-branching-on-the-cheap](https://git-scm.com/book/ko/v1/Git-%EC%84%9C%EB%B2%84-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)

[2] [라즈베리파이 활용 강좌 : Git Server 구축하기](http://www.rasplay.org/?p=1325)

[3] [Installing a Git Server using Apache (WebDAV) on Ubuntu Server 12.04](http://blog.bobbyallen.me/2012/07/23/installing-a-git-server-using-apache-webdav-on-ubuntu-server-12-04/)
