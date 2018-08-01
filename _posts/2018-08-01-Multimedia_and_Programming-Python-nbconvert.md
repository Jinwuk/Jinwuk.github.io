---
layout:  post
title :  "nbconvert를 사용한 google colab export"
date  :   2018-08-01 13:11:00 +0900
categories: [Multimedia and Programming, Python]
tags  :
  - Python
  - nbconvert
comments: true
---

Google colab은 너무나 좋은 Tool이기는 하나, 단독으로는 해당 페이지 (ipynb 파일)을 Markdown으로 Export 할 수 없다. 그러나 Jupyter Notebook을 통하여 markdown으로 export 할 수는 있다.

## Installation
설치전에 가급적 Windows 환경이라면 pandoc과 MikeTeX이 설치 되어 있는 것을 권장한다.  Share LaTeX 덕택에 웹상에서도 간편하게 LaTeX Compile이 가능하지만, 일부 Application들은 여전히 Local Machine에서 LaTeX을 원하는 경우가 많다.

Installation은 간단하다. 일단 Anaconda 환경에서 Intsall 한다는 가정하에 pip 보다는 conda install 위주로 설명한다. 일단, 많은 Python package가 설치 되어 있지 않다고 가정하고 다음과 같이 설치한다.

~~~
conda install nbconvert
~~~

pip 환경에서는 다음과 같이 설치하면 된다.

~~~
pip intall nbconvert
~~~

환경에 따라 추가 설치해야 할 Module들이 있을 수 있다. 설치 Message들을 보면서 설치하면 된다. 보통의 경우 에러 없이 한번에 설치가 된다.

## nbconvert의 사용 및 지원 Format

다음과 같다

* HTML,
* LaTeX,
* PDF,
* Reveal.js HTML slideshow,
* Markdown,
* reStructuredText,
* executable script,
* notebook.

이 중에서 나의 경우는 Markdown을 특별히 더 필요로 한다. 

nbconvert의 경우 잘 설치되면 Jupyter notebook에서 파일->내보내기(export) 를 통해 원하는 포맷으로 내보낼 수 있다.

또한 Command line에서 다음의 형태로 내보내면 된다.
markdown 형태로 export 할 경우 다음과 같이 쓰면 된다.

~~~
jupyter nbconvert --to markdown NLP_Quantization01.ipynb
~~~

## nbconvert 사용/설치시 에러

본인의 경우 2가지 서로 다른 컴퓨터에 설치해 보았는데, 다음과 같은 에러들이 발생했었다. 

### nbformat 문제 

많은 경우, 부딛히게 되는 문제인데, 해당 라이브러리가 설치되지 않거나 버전이 맞지 않아서 발생하는 문제이다. 따라서, 간단히 conda ( 혹은 pip에서) nbformat을 업데이트 하면 된다.

~~~
conda update nbformat
~~~

간단히 다음과 같이 표시되면서 Update 된다. 4.2.0 버전에서 4.4.0 버전으로 업데이트 된다.

~~~
C:\Users\Admin>conda update nbformat
Solving environment: done

## Package Plan ##
  environment location: C:\ProgramData\Anaconda3
  added / updated specs:
    - nbformat

The following packages will be downloaded:
    package                    |            build
    ---------------------------|-----------------
    nbformat-4.4.0             |   py36h3a5bc1b_0         157 KB

The following packages will be UPDATED:
    nbformat: 4.2.0-py36_0 --> 4.4.0-py36h3a5bc1b_0

Proceed ([y]/n)? y

Downloading and Extracting Packages
nbformat-4.4.0       |  157 KB | ############################################################################################################################################# | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
~~~

그 외에 나타날 수 있는 문제들이 몇 가지 있으나 대부분의 문제들은 **nbformat** 과 마찬가지로 해당 라이브러리 혹은 모듈을 설치하거나 업데이트 하는 것 만으로 간단히 해결된다.

## google colab의 Markdown export 

google colab에서 작성한 것을 markdown으로 변환해보자.
우선 다음과 같이 google colab에서 작성된 note가 있다고 가정하자.

<img alt="google_colab" src="/assets/img/google_colab01.png?raw=true" width="600px"/> 

**File->ipynb 다운로드** 를 선택하여 ipynb 파일을 다운로드 받는다.

다음 해당 ipynb 파일 (파일 이름은 노트의 제목이 된다. 여기서는 NLP_Quantization01.ipynb가 된다고 하자)을 Command Line에서 다음과 같이 markdown으로 변경한다.

~~~
jupyter nbconvert --to markdown NLP_Quantization01.ipynb
~~~

NLP_Quantization01.md 파일이 생성됨을 확인한다. 

당연한 것이지만, 생성된 md 파일을 조금 수정하여 Jekyll의 blog로 업로드 하면 된다. 

* 실제 변환된 페이지를 본 블로그에 올려 놓았다. [LINK](https://jinwuk.github.io/multimedia%20and%20programming/python/2018/07/31/Multimedia_and_Programming-Python-NLP_Quantization01.html)

때로는 생성된 md 파일을 Typora(가장 세련된 markdown 편집기) 등에서 열고 pdf등으로 변환하면 자동으로 프로그램에 대한 보고서가 생성된다. 

## Next

향후에라도 google 에서 google colab의 Note를 간단히 웹에서 출력시킬 수 있도록 환경을 업그레이드 할 수 있었으면 한다. 그렇게 어렵게 보이지는 않는데..

