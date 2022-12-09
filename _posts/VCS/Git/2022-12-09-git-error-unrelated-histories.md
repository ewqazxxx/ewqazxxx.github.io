---
title: "[Git][Error] fatal: refusing to merge unrelated histories 에러"
description: 2022-12-09-git-error-unrelated-histories
author: ewqazxxx
date: 2022-12-09 21:00:00 +09:00
categories: [VCS, Git]
tags: [Git]
---
fatal: refusing to merge unrelated histories 에러 내용 정리

<br>

## 상황
원격repo를 연결하고 작업한 로컬repo를 최초로 `git push`
: `error: failed to push some refs to '{원격repo주소}'`: 원격repo로 push 실패
```
PS C:\Users\tt\Desktop\project\githubpage\workspace\ewqazxxx.github.io> git push -u origin main
To https://github.com/ewqazxxx/ewqazxxx.github.io.git
error: failed to push some refs to 'https://github.com/ewqazxxx/ewqazxxx.github.io.git'
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

원격repo로 push 하기전 로컬repo로 pull 필요 `git pull` 실행
: `fatal: refusing to merge unrelated histories` - 관련없는 기록 merge를 거부
```
PS C:\Users\tt\Desktop\project\githubpage\workspace\ewqazxxx.github.io> git pull origin main   
fatal: refusing to merge unrelated histories
```

<br>

## 원인
두 개의 관련 없는 프로젝트가 병합될 때 발생(즉, 서로의 존재를 인식하지 못하고 커밋 기록이 일치하지 않는 프로젝트)

> 기본적으로 `git merge`명령은 실수로 관련 없는 프로젝트를 merge할 때 발생하는 사고를 방지하기 위해 원격repo와 로컬repo 기록을 비교하여 독립적인 기록으로 판단한 경우 git에서 merge를 거부 하도록 설정되어 있다.
[git docs 참조](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---allow-unrelated-histories)

나의 경우 생성한 원격repo와 따로 작업한 로컬repo의 기록이 일치하지 않아 merge가 거부되었다.

<br>

## 해결
merge해야하는 원격repo와 로컬repo 2개의 branch가 따로 작업한 commit기록이 있다면 각각 commit지점을 다시 설정하여 merge를 진행해야 한다.

나의 경우 새로 생성해 비어있는 원격repo라서 merge를 허용해주는 명령어를 입력해 강제 pull로 해결
```
git pull origin main --allow-unrelated-histories
```

<br>

## 개선점
`git clone`으로 로컬repo를 만들어 error 방지할것

<br>

## 참고
 - [Git refusing to merge unrelated histories on rebase](https://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories-on-rebase)
 - ["refusing to merge unrelated histories" failure while pulling to recovered repository](https://stackoverflow.com/questions/39761024/refusing-to-merge-unrelated-histories-failure-while-pulling-to-recovered-repos/39783462#39783462)
  - [git push, pull (fatal: refusing to merge unrelated histories) 에러](https://jobc.tistory.com/177)