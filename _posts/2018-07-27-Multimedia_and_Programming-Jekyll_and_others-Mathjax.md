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


