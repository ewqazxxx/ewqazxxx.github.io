---
title: "[GithubPage] 깃허브페이지 + jekyll템플릿 시작하기(Window)"
description: 2022-12-07-githubpage-start
author: ewqazxxx
date: 2022-12-07 18:50:00 +09:00
categories: [Blog, GithubPage]
tags: [GithubPage]
---
GithubPage 시작하기까지 작업한 내용 정리

<br>

## 설치

### Ruby
> jekyll 템플릿 사용에 필요 

[Ruby 설치](https://rubyinstaller.org/downloads/) - Ruby+Devkit 3.0.5-1 (x64) 받음

### jekyll 템플릿(jekyll-theme-chirpy)
> 템플릿 마다 설치도 다를 수 있으니 본인이 원하는 jekyll 템플릿 검색하여 확인하고 설치 (템플릿에 따라 깃허브 repo에서 직접 fork, zip down 등 여러가지 방법 이용)

[jekyll 템플릿](https://github.com/cotes2020/jekyll-theme-chirpy) - repo에서 zip 파일 받음

### git
> 본인 깃허브페이지 로컬 repo

[git 설치](https://git-scm.com/) - 설치되어 있음

<br>

## 세팅

### 1. Jekyll, Bundler 설치
 - Ruby Prompt창에서 명령어 실행
```
gem install jekyll bundler
```
 - 설치 확인
: `jekyll -v`, `bundler -v`

### 2. Jekyll 템플릿 세팅(jekyll-theme-chirpy 기준)
> 템플릿 마다 상이하므로 사용하는 템플릿의 사용법 참고할것

 - 다운 받은 `jekyll-theme-chirpy.zip`을 본인이 작업할 폴더에 압축 풀기
 : 내 경우 `C:\Users\username\Desktop\project\githubpage\workspace\ewqazxxx.github.io`{: .filepath}폴더에 압축 품

 - 작업할 폴더에서 git bash창 열고 아래 명령어 실행
  : `init.sh`파일에는 템플릿을 초기화 해주는 이것저것 실행 명령어가 존재
  : 쉘스크립트파일(.sh)은 linux에서 사용하는 파일로 window에서는 실행이 안되니 git bash를 이용하여 실행
```bash
$ bash tools/init.sh
```

 - 작업할 폴더에서 cmd창 열고 아래 명령어 차례로 실행
  : 해당 템플릿은 webrick이 없으면 에러남
  : 최종적으로 `bundle install`을 해줘야 필요한 bundle을 설치해줌
```
bundle add webrick
bundle install
```
 - 폴더에 있는 `_config.yml`파일 아래와 같이 수정
  : 아래는 내 기준으로 기본적인 설정들을 수정한 코드만 나열 나머지 코드는 수정x 필요한 경우 확인하고 추가, 삭제, 수정할것

```yaml
lang: ko-KR # 한국어 지원이지만 본인에게 맞게 설정 바꾸고 싶으면 _data>locales>ko-KR.yml에서 수정
timezone: Asia/Seoul
title: ewqazxxx
tagline: TIL # 사이드 메뉴 tag 문구
description: >
  ewqazxxx.github.io
url: 'https://ewqazxxx.github.io'
github:
  username: ewqazxxx
social:
  name: ewqazxxx
  email: ewqazxxx@gmail.com
  links:
    - https://github.com/ewqazxxx
avatar: /assets/img/favicons/apple-touch-icon.png # 사이드 메뉴에 프로필이미지
```
{: file='_config.yml'}

 - 게시물 작성시 `_post` 폴더에 `yyyy-mm-dd-filename.md` 형식으로 파일만들고 작성
  : .md(마크다운)게시물 작성법은 사용하는 템플릿 사용법 참고

### 3. 로컬서버 실행
> 내 작업물을 깃허브에 push하기전에 로컬에서 확인하고 싶은 경우 로컬서버를 실행하며 작업

 - 작업 폴더에서 cmd창 열고 아래 명령어 실행
  : 브라우저 주소 [http://127.0.0.1:4000](http://127.0.0.1:4000)에서 확인
```
bundle exec jekyll serve
```

<br>

## 깃허브페이지 시작

### 1. 원격repo 생성
 - 본인 깃허브 Repositories > New > Repository name에 {username}.github.io 작성하고 create
![githubpage-start-001.PNG](/assets/img/posts/GihubPage/githubpage-start-001.PNG)
_Repository name_

### 2. 원격repo 설정
 - 생성한 원격repo Settings > Pages > Branch를 main으로 변경하고 save
![githubpage-start-002.PNG](/assets/img/posts/GihubPage/githubpage-start-002.PNG)
_Branch_

### 3. 로컬repo 생성하고 원격repo와 연결
 - 작업 폴더에서 cmd창 열고 아래 git 명령어 순서대로 실행
```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin {원격repo 주소}
git pull origin main --allow-unrelated-histories
git push -u origin main
```

### 4. 내 깃허브페이지 접속
 - [https://ewqazxxx.github.io](https://ewqazxxx.github.io)

<br>

## 끝.