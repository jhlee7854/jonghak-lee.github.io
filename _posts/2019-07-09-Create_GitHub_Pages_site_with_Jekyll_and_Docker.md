---
layout: post
title:  "Jekyll과 Docker를 이용한 GitHub Pages 사이트 생성"
date:   2019-07-09
categories: blog
tags: jekyll docker
comments: true
---
이전에 했던 일을 기록을 하지 않으니 항상 잊어버리고 나중에 필요할 때가 되면 다시 웹을 찾아봐야 했다. 이러한 문제를 해결하기 위해 블로그에 내가 했던 일을 기록하여 올려야 겠다는 생각을 했다.

그러면 블로그는 어떻게 시작해야 할까 고민하다가 에전에 잠깐 관심을 가졌던 [GitHub Pages](https://pages.github.com) 생각이 났다.

### GitHub Pages 와 Jekyll
GitHub Pages는 정적인 파일을 서비스해 준다. 자신의 GitHub 계정에 특정 이름(`<자신의 계정명>.github.io`)으로 저장소를 생성하고 해당 저장소에 공개하고 싶은 글을 정적 파일 형태로 생성하여 push하면 된다.

GitHub Pages는 매우 쉽게 자신의 사이트를 만들 수 있지만 사이트를 꾸미거나 컨텐츠를 다양한 카테고리로 분류하여 관리하는 것은 또 다른 문제다. 이러한 문제들을 해결하기 위해 다양한 도구들을 사용할 수 있는데,  [Jekyll](https://jekyllrb-ko.github.io)도 그러한 도구 중 하나이다.

Jekyll은 정적 사이트 생성 도구 이며, [마크다운](https://ko.wikipedia.org/wiki/마크다운) 형태로 컨텐츠를 작성할 수 있다. 또한 자신만의 템플릿을 생성하여 적용하거나 다른 사람이 공개한 템플릿을 자신의 사이트에 적용하는 것도 가능하다.

### Docker를 이용하여 Jekyll 사이트 생성하기
Jekyll은 [Ruby](https://www.ruby-lang.org/ko/)로 구현된 도구이므로 사용하려면 Ruby를 설치해야 한다. 그러나 [Docker](https://www.docker.com)를 이용하면 Jekyll을 사용하기 위해 Ruby를 설치하는 등의 과정을 생략할 수 있어 훨씬 빠르고 간편하게 사용할 수 있다.

Docker를 이용해 Jekyll을 사용하는 방법은 다음과 같다. Docker를 이용하므로 Docker는 당연히 설치되어 있어야 한다.

Jekyll Docker 이미지 가져오기

```bash
$ docker pull jekyll/jekyll
```

Jekyll 컨테이너 실행

```bash
$ docker run --rm -p 4000:4000 -e TZ=Asia/Seoul -v $(pwd):/srv/jekyll -it jekyll/jekyll /bin/bash
```

실행중인 컨테이너 내부에서 Jekyll 프로젝트 생성

```bash
# in the jekyll container
$ jekyll new .
```

실행중인 컨테이너 내부에서 Jekyll 사이트 빌드 명령어

```bash
# in the jekyll container
$ jekyll build
```

실행중인 컨테이너 내부에서 Jekyll 사이트를 서비스할 서버 실행 명령어

```bash
# in the jekyll container
$ jekyll serve
```

Docker 컨테이너가 실행 중인 PC의 브라우저 주소창에 `http://localhost:4000/`을 입력하면 방금 컨테이너를 통해 생성한 Jekyll 사이트에 접속할 수 있다.

이제 컨텐츠가 담긴 소스코드를 `<자신의 계정명>.github.io` 저장소에 push하고 브라우저 주소창에 `https://<자신의 계정명>.github.io`를 입력하면 위에서 생성한 Jekyll 사이트가 GitHub Pages를 통해 서비스 되는 것을 확인할 수 있다.