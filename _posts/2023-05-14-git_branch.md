---
title:  "[Github] git branch와 git merge"
excerpt: "Git을 사용하여 버전을 관리할 때 브랜치를 만들고 병합(Merge)하는 방법에 대해서 알아보자."
categories: Github
tag: [Github, Git_merge, Git_branch]
toc: true
author_profile: false


sidebar:
    nav: "counts"
---

# <span style='color:RGB(135, 203, 206)'>개요
Git으로 소스 코드의 버전 관리를 할 때, 보통 `main` 브랜치는 최종 버전의 소스 코드(실 서비스에 배포된 소스 코드)를 관리하게 됩니다. 그리고, `main` 브랜치가 아닌 브랜치를 생성하고 새로운 기능을 개발한 후, 개발이 완료되면,`main` 브랜치에 `병합(Merge)`하게 됩니다.

[git branch](https://git-scm.com/docs/git-branch)

이번 블로그 포스트에서는 `git branch`와 `git merge`를 사용하여 브랜치를 생성하고 병합하는 방법에 대해서 알아보고, `git log`와 `git diff`를 통해 브랜치간 차이점을 확인하는 방법에 대해 정리하려 합니다.


## 브랜치 확인
---
다음 명령어를 사용하면 현재 로컬(Wroking directory)에 존재하는 브랜치를 확인할 수 있습니다.
``` 
git branch
```
`git branch `명령어를 실행하며 다음과 같이 로컬에 존재하는 브랜치 리스트가 나오며 *는 현재 선택된 브랜치(checkout된 브랜치)를 의미합니다.
```
* main
(END)
```

## 브랜치 생성
---
음 명령어를 사용하면 새로운 브랜치를 생성할 수 있습니다.
```
git branch BRANCH_NAME
```
이렇게 새롭게 생성한 브랜치를 선택하기 위해서는 다음과 같이 git checkout을 사용해야 합니다.

```
git checkout BRANCH_NAME
```

다음 명령어를 사용하면, 새로운 브랜치를 생성함과 동시에 해당 브랜치를 선택할 수 있습니다.

```
git checkout -b BRANCH_NAME
```

## 브랜치 이력 및 차이점 확인
---
   Git에서는 새로운 브랜치를 만들고, 수정한 후, 브랜치의 이력을 확인하거나, 브랜치간의 차이점을 비교할 수 있습니다.

> git log

다음 명령어를 사용하면, 현재 브랜치의 수정 사항을 확인할 수 있습니다.
```
git log
```
다음과 같이 현재 브랜치의 수정 내역이 출력됩니다.

```c
commit cda7cb82ca4b318fe1af3a588e3f958decb3851b
Author: jungo <81670100+jungo0@users.noreply.github.com>
Date:   Thu May 11 18:53:15 2023 +0900

    rest

commit 9d087a0c898dcf68939f2828c30d0c94864141f0
Author: jungo <81670100+jungo0@users.noreply.github.com>
Date:   Thu May 11 18:37:49 2023 +0900

    async
```
여기에 `--branches` 옵션을 사용하면, 로컬에 존재하는 모든 브랜치의 이력을 확인할 수 있습니다.
```
git log --branches
```
다음과 같이 모든 브랜치의 수정 내용이 출력됩니다.

```java
commit eb937a488412661a3fae507d7bef44eacdca4f88 (HEAD -> master, jungo/master)
Author: jungo <81670100+jungo0@users.noreply.github.com>
Date:   Fri May 12 23:59:10 2023 +0900

    callback

commit cda7cb82ca4b318fe1af3a588e3f958decb3851b
Author: jungo <81670100+jungo0@users.noreply.github.com>
Date:   Thu May 11 18:53:15 2023 +0900

    rest
```

다음과 같이 --graph 옵션을 사용하면, 조금 더 이해하기 쉽게 출력됩니다.
```
git log --branches --graph
```

다음과 같이 그래프 형태로 출력됩니다.
```java
* commit cda7cb82ca4b318fe1af3a588e3f958decb3851b
| Author: jungo <81670100+jungo0@users.noreply.github.com>
| Date:   Thu May 11 18:53:15 2023 +0900
| 
|     rest
| 
```

마지막으로 --oneline 옵션을 사용하면, 간단하게 브랜치와 메시지만을 확인할 수 있습니다.
```c
git log --branches --graph --oneline
```
다음과 같이 간단하게 브랜치와 메시지를 확인할 수 있습니다.
```
* cda7cb82 rest
* 9d087a0c async
* c8125633 git-error
```

> git log 브랜치 비교

다음 명령어를 실행하면, 현재 브랜치와 main 브랜치의 커밋 차이를 확인할 수 있습니다.
```
git log main..BRANCH_NAME
```
 main와 특정 브랜치 사이의 차이점을 출력합니다.

`-p `옵션을 사용하면, 수정된 내용도 함께 확인할 수 있습니다.
```
git log -p main..BRANCH_NAME
```

> git diff 브랜치 비교

`git diff` 명령어를 사용하면 좀 더 간단하게 두 브랜치 사이의 차이점을 확인할 수 있습니다.
```
git diff main..BRANCH_NAME
```

## git merge
새로운 브랜치를 만들어, 새로운 기능을 개발하고 완성하였다면, 해당 기능을 `main` 브랜치(실 서버용 브랜치)에 병합(Merge)하여 새로운 기능을 사용자에게 제공해야 합니다.

그럼 새롭게 개발한 기능을 포함하고 있는 `BRANCH_NAME`를 `main` 브랜치에 병합하는 방법에 대해서 알아봅시다. `BRANCH_NAME`를 `main` 브랜치에 병합하기 위해서는 우선 `main` 브랜치로 이동할 필요가 있습니다.
```
git checkout main
```
그런 다음,` git merge` 명령어를 사용하여 `main` 브랜치에 병합하고자 하는 브랜치를 병합합니다.
```
git merge BRANCH_NAME
```

브랜치가 무사히 병합되면 다음과 같은 메시지를 확인할 수 있습니다.
```
Merge made by the 'recursive' strategy.
 example.txt | 1 +
 1 file changed, 1 insertion(+)
 ```
마지막으로, 다음 명령어를 사용하여 병합된 브랜치를 제거합니다.
```
git branch -d BRANCH_NAME
```
여기서 사용한 `-d` 옵션은 병합된 브랜치를 지울 때 사용합니다. 만약, 병합되지 않은 브랜치를 제거하고자 한다면 `-D` 옵션을 사용해야 합니다.
```
git branch -D BRANCH_NAME
```

