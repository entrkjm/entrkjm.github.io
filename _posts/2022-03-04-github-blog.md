---
layout: post
title: 삽질에 삽질을 거듭하고 깃허브 블로그 만들기
date: 2022-03-04 04:08:00 +/- 0000
categories: [github, blog]
tags: [github, blog, jekyll]     
author: entrkjm
---


# Github로 블로그 만들기

네이버 블로그, 티스토리, 브런치...나는 여러 플랫폼에 글을 써왔으면서도 내가 쓰는 글이 어떤 절차로 어떻게 올라가는지, 어디에 저장되는지, 사람들은 어떻게 내 글을 볼 수 있는지 잘 몰랐었다. 네이버나 티스토리에서 지원하는 에디터는, 굳이 내가 글을 쓰고 편집을 어렵게 하지 않아도 예쁜 형태의 포스트로 만들어주었으며, 네이버 등 회사의 서버는 나의 글을 저장해서 편히 누구든 요청만 하면 접근할 수 있도록 도와주었다.

**그렇지만 웹 사이트의 호스팅 원리에 대해서 간단하게 알고나니, 그동안 내가 얼마나 쉽게쉽게 살았는지를 실감한다.** 도메인 구매도, 호스팅도 모두 돈이 드는 일이고 간단한 웹페이지를 만드는 일조차 나에겐 쉽지 않다. 다른 사람이 내 홈페이지를 보는데에는 그 전에는 몰랐던 복잡한 절차가 숨어있었던 것이다.

**그래서 깃허브가 제공해주는 호스팅 서버를 받고, 동시에 Jekyll이라는 테마를 활용하여 블로그를 만들어보면서, 이를 간단히 경험해보기로 했다.** 중간에 삽질이 굉장히 많아 이틀을 꼬박 사용했지만, 만들기 전에 반드시 알아두어야할 핵심 포인트만 짚으면 다음부터는 어렵지 않을 것으로 보인다.
  
---

## 블로그 만들기 전 숙지해야할 점

우선 반드시 숙지해야할 포인트는 다음과 같다.

1. **개발을 하며 깃허브에 코드를 올리기 전, 우리는 로컬 저장소에서 작업을 한다.**  
2. **깃허브 블로그를 만들기 위한 Template은 Jekyll이라는 라이브러리로 이루어져 있으며, 이는 Ruby라는 언어로 작성되어있다.(사실 Ruby를 자세히 알 필요는 없다.)**

---

## 블로그 만들기 절차
  
이 두 포인트를 숙지한다면, 우리의 블로그 만들기 절차는 반드시 다음을 따라야한다.

1. **내가 사용하고자 하는 Jekyll Template 파일들을 로컬 컴퓨터에 옮긴다(깃허브로 Fork하든, Install을 하든...)**  
2. **Jekyll Template을 활용하여 자신에게 맞게 Customize 한 다음에, 이를 Github이 호스팅할 수 있는 형식에 맞추어 Github 저장소에 Pull한다.**
3. **자신의 Github 저장소에서 호스팅 절차를 밟는다.**

---

## 발생하는 문제들

문제는 이 3단계 스텝 사이사이에서 발생한다. 

1)에서: 일단 내가 사용하고자 하는 테마는 [**chirpy**](https://chirpy.cotes.page/)이었는데, **이 테마를 그냥 다운 받아서 설치하면 높은 확률로, 2)에서 오류를 낳는다.** 

그렇기 때문에 제작자분이 Github에 만들어 두신 [**Starter 템플릿**](https://github.com/cotes2020/chirpy-starter)을 활용하여 내 Repository를 만들고, 그걸 내 로컬 저장소로 fork해오는 방식이 먹혔다. (Starter 템플릿 외에, 저 개발자분이 만드신 다른 [**Repository**](https://github.com/cotes2020/jekyll-theme-chirpy)는 뭔가 이슈가 있어서 내 로컬 저장소로 clone해도 잘 작동하지 않는 것 같다.)

2)도 문제다. Jekyll Template를 수정하기 위해서는 Template에 따라 다르지만, Ruby를 설치하고 Bundler와 Jekyll이라는 라이브러리를 주로 활용해야하며, 이 외에도 다양한 Plug-in들이 들어간다. **근데 이 Plug-in들도 각기 버전이 있어서, Ruby 버전이나 Bundler, Jekyll 버전과 계속 충돌할 수가 있다. 이렇게 충돌하게 되는 경우 아예 Template를 수정하기가 어렵다.** 

왜냐면 내가 Github로 호스팅하기 전에 로컬에서 이런저런 테스트도 하고, 커스터마이징도 해야하는데 그 절차를 밟기가 너무 어려워지기 때문이다. Template를 만드신 제작자께서 친절히 설명해주시면 좋은데, Jekyll 문서를 참조하라는 식으로 퉁쳐놓은 것들이 많아서 쉽지 않다. (참고로 Ruby에서 설치하는 라이브러리들을 Gem이라고 부르는 듯 한데, 이 수많은 Gem들의 버전을 고려해서 형식을 맞추려면 여간 빡치는 것이 아니다. 기왕이면 Template 만드는 분이 해두신 절차를 따라가는게 제일 좋다.) 간단한 기능만 제공하는 Template면 괜찮은데, 복잡한 기능을 지원하는 경우에는... 이런 일이 빈번히 생길 것이다.

3)의 경우 Github에 익숙하다면 별다른 문제가 되지 않을 것이다. 다만, 내가 사용하는 chirpy테마의 경우 로컬에서 수정한 내 블로그를 push하기 전에 사전에 작업해둬야할 것이 있다. **내가 사용하는 테마를 만드신 분께서는, 내가 remote branch에 push할 때에 자동으로 'gh-pages'라는 branch를 만들 수 있도록 자동화해두셨고, 나는 이 branch를 호스팅해야한다고 적어두셨다.** [**링크**](https://chirpy.cotes.page/posts/getting-started/)

이 테마에 대한 자세한 지식은 Read.md에는 별로 없고, [**데모 사이트**](https://chirpy.cotes.page/)의 포스트 중에서 'getting-started'라는 설명서가 있는데 이걸 따라하는게 최선이다. 쥐엔장... 너무 불친절해서 어떤게 설명서인지조차 찾아야하는게 개빡친다.

---

## 정리 및 여담

여튼 1) 업데이트가 잘 돼서 충돌하지 않을 Template 파일들을 내 로컬 저장소로(절차에 맞게) 잘 가져오고 2) Jekyll에서 정한 룰에 맞게 '_config.yml' 파일을 잘 수정해주면서 Custominzing하고, 3) Github에 잘 호환되도록 제작자님이 정한 룰에 맞게 잘 호스팅하는 것이 최선이다. **이게 블로그 만들기의 전부이고 핵심이다.**

여담1) 그렇다면 블로그에 글은 어떻게 쓸까? 우선 로컬 저장소에서 Jekyll의 룰에 맞게 md 파일을 만들고, 그걸 post 폴더에 두면 된다. 그리고 이를 remote에 push하면 내 로컬 저장소에서 변경된 사항이 remote에 반영되고, 반영된 내용이 호스팅되는 형식이다. 캬. 평상시 네이버 블로그에 글쓰는 것을 생각하면...이와 반대일 것이다. 

에디터가 삽입된 네이버의 웹페이지에 내가 글을 쓰고, 그 글이 네이버의 데이터베이스에 저장돼서 누군가가 내 블로그에 방문해서 글을 볼 때마다 호출될 수 있도록 연결이 유지되어 있어야 할 것이다. Github 블로그에서는 내가 내 데이터베이스를 수정해서 글을 쓰고 그 글이 remote를 통해 반영되면 github에서 이에 접근할 수 있도록 연결해준다.

**블로그에 글을 쓸 때는 GIt의 버전 관리를 이용하면 좋다.** 우선 글을 써서 파일을 업데이트할 Branch를 하나 정해놓고, 그걸로 push한 다음에 잘 되면 'master' branch에도 merge하거나 pull 받거나 하는 방식을 쓴다. 이러면 오류가 나도 master branch는 이전 버전에 있기 때문에, 여기서부터 다시 시작하기 편하다.

여담2) Jekyll은 꽤 좋은 것 같다. 직관적으로 잘 이해된다. 단순한 기능만 잘 익힌다면 그리 어려운 것은 없는 듯 하다.