---
layout: "post"
title: "[Web] 시맨틱 태그(Semantic Tag)에 관하여"
date: "2017-12-08 11:19"
category: Web
tags: Web HTML5
---

## Background

현재 진행하고 있는 [Django기반의 프로젝트](https://kirade.github.io/blog/tags/#Django)에서 사용하고 있는 HTML페이지는 현재 일반적으로 사용이 되고 있는 HTML5의 개념들을 대부분 따르지 않고 있다. 그 중, 가장 대표적인것은 HTML5에서 대표되는 시맨틱 태그(Semantic Tag)의 부재이다.

웹을 공부하면서 자주 참고하고있는 W3School에서 정의한 시맨틱과 관련된 정의는 이렇다.
>Semantics is the study of the meanings of words and phrases in a language.
>
>Semantic elements = elements with a meaning.

즉, 시맨틱(Semantics)이란 언어의 단어와 구절의 의미에 관한 연구이며, 시맨틱 요소(Semantic element)라고 하는것은 의미를 가지고있는 요소이다.

따라서, 여기서 HTML5의 특징으로 보는 정의해 볼 수 있는 Semantic Tags는 이와 같은 맥락에서 `의미를 가지고 있는 태그의 단위`정도로 이해를 한다면 적절할 것으로 보인다.

---

## Study

![시맨틱 태그(Semantic Tags )](https://kirade.github.io/images/2017/12/semantic_tags.gif){: .center-image}

### 1. Tags  
시맨틱 태그는 위에 첨부되어 있는 이미지에 볼 수 있는 주요 태그들 이외에도 다양한 태그가 존재한다. 각 태그의 의미를 해석할 때에는 시맨틱이라는 의미론적인 정의에 걸맞게 태그의 의미를 해석하는것이 도움이된다.
여기서 모든 시맨틱 태그를 소개하지는 않지만 주요하게 사용하는 태그들을 소개합니다.

  - `<article>`
  : 관심사에 따라서 글을 작성하기 위해 작성되는 독립적인 요소입니다. 또한, `<h1> ~ <h6>`의 제목 요소를 가지는 것을 권고한다.
  - `<aside>`
  : 주요한 주제가 아닌 부차적인 내용을 담는 태그입니다. `<article>`태그안에 들어갈 수도있고 외부에 존재할 수도 있습니다. 외부에 존재하는 경우 기존의 `<div class=sidebar>`과 같은 역할을 한다.
  - `<footer>`
  : `footer`라는 이름에서 알 수 있듯, 웹페이지의 발 부분, 즉 하단을 나타내는데 사용되는 태그이다. 웹페이지의 저작권, 상표, 연락처, 회사 주소와같은 웹 페이지의 메인 컨텐츠는 아니지만 게시되어야 하는 부가적인 정보를 가지는 태그이다.
  - `<header>`
  : `<head>`태그는 `<body>`태그 이전에 쓰이는 HTML태그이지만 `<header>`태그는 `<body>`태그 안에서 제목 혹은 머리말을 표현하기 위해 사용되는 태그이다.
  - `<main>`
  : 페이지의 메인 컨텐츠를 담는 태그이다. 한 페이지에 한번 쓰일 수 있다.
  - `<nav>`
  : '네비게이션 바'라고 불리는 메뉴바와 같은 것들을 포함하는 태그이다.
  - `<section>`
  : 관심사에 따라서 구획을 구분하기 위한 태그이다. 이 또한 `<article>`태그와 같이 `<h1> ~ <h6>`의 제목태그를 담는것을 권고한다. 이를 통해  해당 섹션의 관심사가 무엇인지 검색 로봇에 알려줄 수 있다.

### 2. Meanings
  웹 페이지의 소스코드 부분은 겉으로만 이쁘게 보인다면 웹 페이지를 사용하는 사용자에게는 문제가 되지 않는다. 하지만 웹 페이지를 만들어내는 기계는 소스코드에서 태그의 내용에 따라 내용을 추출하여 사용자에게 보여준다.

  따라서, 검색 엔진이 데이터를 효율적으로 추출하여 더욱 의미있는 검색결과를 만들어 내기 위해서는 태그에 의미를 담아 검색엔진이 이해할 수 있도록 돕는것이 좋은 방법일 수 있다.  

  또한, 검색엔진은 물론 각 태그의 의미를 명확하게함으로써 웹 사이트에 접근성을 높이는 의미있는 결과를 낳을 수 있다. 예를 들면, 시각장애인과 같은 경우 듣는것으로 의존하여 웹을 사용하는데 이때, 적절하게 시맨틱 태그가 연결되어 있다면, 해당 부분이 어떤 내용이고 어떤 의미를 담고 있는지 올바르게 선별하여 들어볼수 있는 높은 접근성을 제공할 수 있다.

---

## Reference
* [W3Schools - HTML5 Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)
* [So Eun Lee - 시맨틱하게 HTML을 짠다는 것](https://medium.com/@soeunlee/%EC%8B%9C%EB%A7%A8%ED%8B%B1%ED%95%98%EA%B2%8C-html%EC%9D%84-%EC%A7%A0%EB%8B%A4%EB%8A%94-%EA%B2%83-90612ffc988e)
