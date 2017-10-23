---
layout: post
title: Jekyll Github Page의 SEO
comments: true
---
지금부터 검색엔진 및 SNS를 통해 Jekyll로 포스트 되는 블로그가 더욱 잘 검색될 수 있도록 도와주는 SEO Tag에 대해서 알아보자.

## Jekyll SEO Tag 설치
1. root 폴더에 위치한 _config.yml 에 다음의 plugin 사용을 위한 구문을 정의한다. 

~~~
plugins:
  - jekyll-seo-tag
~~~

2. </head> tag 바로 이전에 다음 구문을 추가한다. 나의 경우에는 _includes/head.html에 다음과 같이 정의했다.

~~~
<head>
  ..
  <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Libre+Baskerville:400,400i,700">
  {% seo %}
</head>
~~~

위의 간단한 과정만으로 SEO Tag 사용을 위한 정의가 끝난다.

## Jekyll SEO Tag가 하는 일

우선 Jekyll SEO Tag의 설치 전과 후를 Chrome Dev Tool의 소스보기를 통해 비교해 보면,

- 설치 전

![1](../assets/image/2017/10/23/1.png)

- 설치 후

![2](../assets/image/2017/10/23/2.png)

한눈에 봐도 여러 종류의 meta tag들이 head tag 안에 추가된 것을 확인할 수 있다.
즉 SEO Tag 를 사용하면 meta 태그를 자동으로 생성해주면서 포스트가 검색엔진에 더욱 잘 노출될 수 있도록 도와주는 역할을 한다.  

### title

Site 제목이 추가된 형태로 포스트의 title 태그를 생성한다. 
title 태그는 검색엔진의 검색결과의 제목으로 표시되는 내용이다.
~~~
<title>Jekyll Github Page의 SEO | Software Holic</title>
~~~

### description

페이지에 대한 짧은 설명을 제공하는 태그로, 검색결과에 나타나는 Snippet 일부로 사용할 수 있다.
~~~
<meta name="description" content="blog" />
~~~

## Canonical URL

## Rich 인덱싱을 위한 JSON-LD Site, post metadata 

## OG(Open Graph) title, description, site title, and URL (for Facebook, LinkedIn, etc.)

[오픈그래프](http://ogp.me/)

## 참고자료

 - [GitHub Help](https://help.github.com/articles/search-engine-optimization-for-github-pages/)
