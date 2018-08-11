Google Adsense 적용
===================

의외로 간단하다.\
**Google Analytics** 의 적용방식을 참고하여 만들면 된다.

-   먼저 다음의 Google Adsense code (맨 처음, Mail을 통해 받게 된다.)를
    가지고 **google\_adsense.html** 을 만든다.

<!-- -->

    <code class="html">
    <!-- google_ad_client: "ca-pub-2352406350095521" -->

    {% if jekyll.environment == 'production' and google_ad_client %}
    <!-- google Adsence -->
    <script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
    <script> (adsbygoogle = window.adsbygoogle || []).push({
    google_ad_client: "{{ site.google_ad_client }}",
    enable_page_level_ads: true
    });
    </script>
    {% endif %}
    </code>

-   if 문이 들어간 것은 google adsense를 적용하지 읺기 위해서는 단순히
    \_config.yml에서 해당 파라미터를 지우면 되기 때문이다.
-   google\_ad\_client의 값을 \_config.yml을 통해 받기 위해 다음과 같이
    \_config.yml에 파라미터를 추가한다.

<!-- -->

    <code class="ruby">
    google_ad_client: ca-pub-2352406350095521
    </code>

-   그 다음, google\_analytics.html 이 적용된 html을 찾아본다.
    -   해당 파일은 Hydeout Theme에서는 \*head.html\*에 다음과 같이
        적용되어 있다.

<!-- -->

    <code class="ruby">
      <title>
        {% if page.title == "Home" %}
          {{ site.title }}{% if site.tagline %} &middot; {{ site.tagline }}{% endif %}
        {% else %}
          {{ page.title }} &middot; {{ site.title }}
        {% endif %}
      </title>

      {% include google-analytics.html %}
    </code>

-   여기에 다음과 같이 Google Adsense를 적용시킨다.

<!-- -->

    <code class="ruby">
      <title>
        {% if page.title == "Home" %}
          {{ site.title }}{% if site.tagline %} &middot; {{ site.tagline }}{% endif %}
        {% else %}
          {{ page.title }} &middot; {{ site.title }}
        {% endif %}
      </title>

      {% include google_adsense.html %}
      {% include google-analytics.html %}
    </code>

post.html 파일에 Debug Code를 넣고 테스트 해보면 된다.

참고 사이트
-----------

[Jekyll 애드센스 승인받기 (포스팅
22개)](http://leechoong.com/posts/2018/jekyll_adsense/)\
[Google Analytics & AdSense for Jekyll
Blogs](https://flipdazed.github.io/blog/website/google-adsense-and-google-analytics)
