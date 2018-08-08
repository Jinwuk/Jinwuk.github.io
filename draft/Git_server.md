
Windows 에서 Git server 설치 
====

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
  
Windows에 HTTP 서버 서비스를 구현하는 가장 간단한 방법은 **Bitnami**에서 제공하는 Apache 서버 솔루션을 설치하고 그 위에서 Git 서버를 구현하는 것이다. ([Bitnami App Catalog Link](https://bitnami.com/stacks))  혹은, 아예 Apache Home Page에서 Windows용 Apache 

대체로 Bit

많은 경우, Windows의 Apache 서버 세팅 대신 Linux Apache 서버 세팅인 관계로 Windows에서 어떻게 Git 서버 세팅이 가능한지, 잘 나와 있지 않다.  그러나 생각보다 쉽다.

 

일단 서버의 경우 다음과 같이 bare Git Repository를 htdocs에 만든다.

 

이 두 명령어는 Windows Commander로 만들고

~~~
mkdir test_git.git
cd test_git.git
~~~
 

git 명령은 Windows용 Git Bash를 사용해야 한다. 디렉토리는 test_git.git 이다.

~~~
git --bare init
git update-server-info
~~~
 

즉, Command 창과 Git Bash 창을 동시에 사용해야 한다.
다음 WebDav를 활성화 시켜야 한다. 2가지 방법이 있다.

 

1.     Windows IIS 로 WebDav를 활성화 시키는 방법 (그런데 이방식으로 Apache 서버가 활성화 되는 것 같지 않다.)

Windows 7 에서 Webdav 서버 설정하는 방법

http://ycho.tistory.com/15

제어판->Windows 기능 활성/비활성 -> IIS (Internet Information Service)기능 활성화

 

2.     Apache의 WebDav 모듈을 Enable 시키는 방법

a2enmod dav_fs

그런데 보통은 a2enmod.exe 가 Redmine Apache 서버에 없다 그럼 다르ㅡㄴ 방법은??

 

3.     httpd.conf 에서 WebDav 활성화 시키기

일단, Apache 서버를 끄고

/conf/ httpd.conf   에서 다음을 찾아보자.
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

DocumentRoot "C:/Bitnami/redmine-2.4.2-0/apache2/htdocs"

로 설정되어 있고 해당 Root의 형식이 그 밑에 설정되어 있다.

나중에 환경변수로 Git Repository 를 설정하고 비슷하게 만들어서 실험해 보자.

 

그 다음 Password File을 생성해야 한다. Bin 밑에 보면 htpasswd 가 있다. 이것을 사용하여 다음과 같이 만들자.

$ htpasswd -c passwd.git <user>

 

그러면 password 를 묻는다. Password를 입력하면 passwd.git 파일이 생성된다.

passwd.git 파일을 /conf 밑에 복사한다.

사용자를 추가하기 위해서는 위에서 passwd.git 에 –c 옵션 없이 사용자를 추가하면 된다.

 

다시, httpd.conf 파일을 열어서 다음과 같이 편집한다.

 
~~~
# WebDAV for Git Server
# First Locking DAV Operation using DavLockDB
# Second Including the following Directory
#

DavLockDB  "c:\Bitnami\redmine-2.4.2-0\apache2\var\DavLock"

<Location /test_git.git>
     DAV on
     AuthType Basic
     AuthName Git
     AuthUserFile conf/passwd.git
     Require valid-user
</Location>
~~~
 

DavLockDB 경로를 잘 적어 주어야 한다.

User의 경우 valid-user로 해주어야 한다.

Apache 서버를 다시 Enable 시킨다.

이 정도만 하면

http://jnwhome.iptime.org/test_git.git 하면 해당 페이지를 볼 수 있다 (ID와 PW 입력 후)

 

그리고 가장 중요한 점은…

Test_git.git 폴더의 권한을 잡아 주어야 한다. Linux에서는 이 부분을 chmod 혹은 chown -R www.www 을 통해 수행하는데 Windows 에서는 전혀 다르다. Windows에서는 Exploere 에서 git Repository인 test_git.git 에 우측 마우스를 대고 **속성->보안**으로 들어가서


**Authenticated Users**를 **모든 권한**으로 해 주어야 한다. 안 그러면 Git 에서 에러가 난다. 이로서 **WebDav로 인증된 사용자가 Git Remote 서버를 인증하여 사용**할 수 있게 된다.

 

Client 에서는??

만일 Git Bash가 있다면 다음과 같이 하면 된다. (경로는 Windows 경로가 되도록 한다)

 

mkdir ~/Desktop/test-project

cd ~/Desktop/test-project

git init

git remote add origin http://<user>@<server name or IP address>/test-project.git

touch README

git add .

git commit -a -m “Initial import”

git push origin master

 

만일 TortoiseGit 이 설치되어 있다면 다음과 같이 한다.

일단, Git Repository here 를 수행하여 특정 폴더를 git Repository 로 만든다.

Bare로 만들면 안된다.

TortoiseGit -> Setting -> Git 에서 설정을 확인한 후 (사용자 정보와 이메일)

Git->Remote를 설정한다. (매우 중요)

<URL>

http://jnwhome.iptime.org/test_git.git

 

이것만 넣어 주어도 자동적으로 origin 이 뜬다. 다음이 중요하다.

 

<Push URL>

http://MyID:MyPW@jnwhome.iptime.org/test_git.git

 

꼭 ID와 PW를 http:// 앞에 같이 써주어야 한다.

그리고 PUSH를 해주면 Remote에 Push가 된다.


## Reference

본 내용과 관련하여 기본적인 사항은 다음 사이트를 참조한다.

[1] [Git --local-branching-on-the-cheap](https://git-scm.com/book/ko/v1/Git-%EC%84%9C%EB%B2%84-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)

[2] [라즈베리파이 활용 강좌 : Git Server 구축하기](http://www.rasplay.org/?p=1325)

[3] [Installing a Git Server using Apache (WebDAV) on Ubuntu Server 12.04](http://blog.bobbyallen.me/2012/07/23/installing-a-git-server-using-apache-webdav-on-ubuntu-server-12-04/)
