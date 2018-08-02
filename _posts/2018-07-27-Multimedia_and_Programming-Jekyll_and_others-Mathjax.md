---
layout: post
title:  "Jekyll에 MathJax Embedding 시키기"
date:   2018-07-28 17:44:00 +0900
categories: [Multimedia and Programming, Jekyll_and_others]
tags:
  - Mathjax
comments: true
---

* Table of Contents
{:toc}


## Mathjax 세팅

먼저 다음과 같이 해야 한다. \_config.yml의 Markdown Processing Setting에서
~~~~ yml
    kramdown:
      math_engine:       mathjax
      math_engine_opts:
        preview:         true
        preview_as_code: true
~~~~


`_layouts\post.html` 에 다음의 MathJax Rendering 코드를 첨가한다.

- 원본 `post.html`

![](http://jnwhome.iptime.org/redmine/attachments/download/807/picture839-1.png)

- 다음의 MathJax Code 를...

~~~~ html  
<script type="text/x-mathjax-config">
       MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});
    </script>
    <script type="text/javascript" async
      src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
    </script>
~~~~

- 이렇게 삽입해야 한다.

![](http://jnwhome.iptime.org/redmine/attachments/download/808/picture632-1.png)

## 추가사항
### Jekyll HTML Renderer 문제
본 항목을 작성하면서 Jekyll 의 @<pre></pre>@ 기능에 문제가 있는 것을 확인하였다.
Markdown에서는 code 를 표시하기 위하여 @~~~~ code // ~~~~@를 사용하고, 웬만한 HTML Paser에서도 정상 동작하지만, Jekyll에서는 이 부분이 제대로 동작하지 않음을 확인하였다.

처음에는 Kramdown Markdown 엔진의 문제인 것으로 생각했으나, Kramdown에서 제공하는 Markdwon Web 편집기에서도 정상 동작하는 것을 확인하여 Kramdown의 문제가 아니라, Jekyll의 HTML Renderer의 문제임을 확인하였다.

관련 post를 찾아 본 결과 여전히 해당 문제는 해결되지 않음을 알 수 있었다,

이 때문에 대부분의 HTML 코드들은 그림으로 처리되어 있어, 상요자가 간단히 코드를 복사해서 사용하기에는 문제가 있다. 해당 문제에 대한 해결책은 계속 찾아 보도록 하겠다.

### MathJax or KaTex

MathJax는 LaTeX의 거의 모든 항목을 Rendering 할 수 있으나 속도가 느리다는 단점이 있다, 반면, KaTeX의 경우는 속도는 빠르나 LaTeX의 항목을 모두 Rendering 하지 못한다는 문제점이 있다.

본 페이지는 현재 Kramdown에서 KaTeX을 사용하도록 세팅되어 있다.
KaTeX 사용에 대해서는 다음 포스트에서 논하도록 하겠다.

### Latex 사용시 주의할 점

Typora, Haroopad등 대부분의 Markdown Editor에서 전혀 문제가 되지 않지만, Jekyll을 사용하여 Post할 때 문제가 되는 몇가지 LaTex 표현들이 있다.

본인이 직접 겪은 문제들은 다음과 같다.

* $$x^{*}$$ 표현
   - LateX 기호로 ^{*} 의 표시가 Jekyll에서는 수식으로 잘 인식이 되지 않는 문제점이 있다. 즉, 다음과 같이 표시할 때 문제가 된다.

~~~latex
$x^{*}$
~~~

이 경우 해결은 의외로 간단하다. 달러 표시 하나로 되어 있는 것을 2개로 바꾸어 주면 된다.
대부분의 Markdown Editor/Viewer 에서 달러표시 2개 표시는 수식 Box 로 인식되나. Jekyll에서는 그렇게 인식되지 않는다. 수식 box의 경우는 반드시 아래, 위 1칸을 빈칸으로 두어야 한다. 따라서 Inline에서 LaTeX 수식을 삽입할 때 $ 하나만 있을 경우, 수식으로 인식하지 못하는 경우가 있어 이러한 문제가 발생한다.

해결책은 간단한데, 달러 표시 하나를 두개로 바꾸는 것이다.

~~~latex
$$x^{*}$$
~~~

* $\mid x \mid$ 표현

LaTeX 기본이나, 혹은 대부분의 markdown에서 문제가 되지 않는 세로줄 표시가 Jekyll에서는 문제가 된다. 이것 역시 Inline에서 문제가 되는 것으로서 Inline에서 LaTeX의 특정 기호가 수식으로 인식되지 못하는 까닭에 발생하는 것이다. (Kramdown Markdown rendere의 Bug?) 

즉, 다음과 같이 표시하면 제대로 표현이 되지 않는다.

~~~latex
$|x|$
~~~

궁여지책으로 이때는 LaTeX의 \mid 를 사용해야 한다. 즉, 다음과 같이 써 주어야 한다.

~~~latex
$\mid x \mid$
~~~

이 외에 다른 문제점은 발견 되는대로 이 페이지에 올리도록 하겠다.
