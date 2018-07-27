---
layout: post
title:  "Hydeout Theme 꾸미기"
date:   2018-07-27 03:09:00 +0900
categories: [Multimedia and Programming, Jekyll_and_others]
tags:
  - Jekyll
comments: true
---

* Table of Contents
{:toc}


본 블로그에 적용된 Theme는 Hydeout 이라는 Theme이다. 이 Theme의 특징은 매우 단순하면서도, Jekyll의 기본 Directory 구조를 거의 그대로 따라가고 있기 때문에, 다른 Theme에서도 본 Theme에서 사용된 기법들을 거의 그대로 적용할 수 있다는 장점이 있다.

물론, 각 Theme별로 Directory내에 존재하는 Theme 구현을 위한 HTML 파일들의 구체적인 코드들은 다를 수 있다.
그러나, 본 Theme의 경우는 매우 빠른 시간에 Theme 구성을 위한 HTML 파일들을 쉽게 이해할 수 있으며, 동시에 비교적 HTML 파일들의 종속 구조가 잘 구성 되어 있어, 다른 Theme 나 Jekyll 자체의 변화를 잘 적용시킬 수가 있다.

Hydeout Theme를 꾸미는데 있어 맨 처음으로 하는 것은 원래 검정색 계통인 Hydeout Theme의 Sidebar 부분의 색상을 변화 시키는 것을 해 본다.
이를 통해 Hydeout Theme 및 Jekyll의 구조에 대하여 익숙해질 수 있도록 한다.

sidebar.html 분석
-----------------

Jekyll의 kramdown markdown renderer는 HTML 파일에 대한 Code block을 올바로 Parsing 하여 rendering 하지 못한다. 따라서 Typora에서 코드를 Parsing 한 후, 이것을 PNG로 변환하여 코드를 올리는 수 밖에 없다. 다음은 그 결과이다. 

![](http://jnwhome.iptime.org/redmine/attachments/download/805/picture593-1.png)

-   여기서 `{{ xxx }}` 로 나타나는 부분이 Hydeout의 변수 부분이다.
    -   **site.xxx** 로 나타나는 변수는 \_config.yml 에서 수정하거나
        첨가하면 된다.

각각의 변수는 다음의 의미이다. (그림 참조)

![](http://jnwhome.iptime.org/redmine/attachments/download/803/2018_0725_0001.png)

Back ground 색상 변화
---------------------

`_sass\hydeout\_variables.scss` 에서,

~~~ ruby
    // Hyde theming
    $sidebar-bg-color: #202020 !default;
    $sidebar-title-color: #ffffff !default;
    $sidebar-sticky: true !default;
    $layout-reverse: false !default;
    </code>
~~~

`$sidebar-bg-color` 항목을 이렇게 바꾼다.

~~~ ruby
    // Hyde theming
    //$sidebar-bg-color: #202020 !default;
    $sidebar-bg-color: #106792 !default;
    $sidebar-title-color: #ffffff !default;
    $sidebar-sticky: true !default;
    $layout-reverse: false !default;
    </code>
~~~