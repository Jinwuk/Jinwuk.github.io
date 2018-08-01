nbconvert를 사용한 google colab export
=====

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


## nbconvert 사용시 에러

본인의 경우 