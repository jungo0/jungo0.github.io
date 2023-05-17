---
title:  "[Github] git 명령 취소하기"
excerpt: "Git에서 명령을 취소하는 여러 방법을 알아보자"
categories: Github
tag: [Github, Github명령취소 ]
toc: true
author_profile: false


sidebar:
    nav: "counts"
---


**git에서 여러가지 취소하고 싶을 때**

여러가지 케이스 별로 대응 하는 `git명령어` 모음!

## 1. 로컬 변경 취소
```
$ git checkout .
```
신규 추가한 파일에 관해서는 삭제되지 않으므로, 완전히 원래대로 되돌리려면 따로 삭제해야 한다.
```
$ git clean -df .
```
## 2. add를 취소
```
$ git reset HEAD .
```
이것만 하면 add 상태밖에 취소되지 않기 때문에,
다른 변경도 취소하고 싶으시다면, 1. 로컬 변경 취소 작업도 할 필요가 있다.


## 3. commit 취소
```
$ git reset .
```
mode의 디폴트는 `--mixed`이기 때문에
변경한 파일은 모두 그대로이고 git의 이력만 바뀔 뿐.

변경한 파일을 포함하여 모두 지정된 commit상태로
되돌리고 싶은 경우 mode에 `--hard`를 지정한다

또, 이쪽도 `--hard`를 지정했다고 해도 신규 추가 파일은
남은 채로 있기 때문에
완전히 되돌리려면 별도로 삭제해야 한다
```
$ git reset --hard <commit_Id>
```
## 4. push 취소
```
$ git revert <commit_Id>
$ git push
```
이것은 undo한다는 느낌 보다는
지정된 commit까지의 변경 지점을 `commit`하는 것.
그렇기 때문에 revert 뒤에 push 하는 걸로 Remote가 실질적으로 undo를 한 것 같은 상태가 된다.

복수의 커밋을 취소하고싶을때는
`-n`옵션으로 지정할 수 있다.
```
$ git revert -n <commit_Id>
$ git revert -n <commit_Id>
...
$ git commit
$ git push
```

`-n`은 `--no-commit`과 동일한 옵션

<span style='color:RGB(135, 203, 206)'>**git merge했지만 역시 그만두고 싶을 때의 방식 4종류**


## 1. git 머지(병합) 했더니 충돌 역시 그만 둬야지!
충동을 편집해서 수정하지 않을 경우 한정
```
$ git merge --abort
```
병합전의 상태로 되돌린다.

## 2. git 머지(병합) 했더니 충돌해서 수정하려고 시도했지만, 중간에 그만두고 싶을때
```
$ git reset --hard HEAD
```
편집한 내용도 머지(병합)도 모두 취소됩니다.

## 3. 머지(병합) 모두 완료했다. 근데 역시 되돌리고 싶을때. : case1
`revert` 커맨드를 사용하여 Merge commit을 취소합니다.
```
$ git revert -m 1 <merge_commit>
```
마지 커밋의 경우 부모가 두 가지로 나뉩니다.
`revert` 명령어를 사용할 경우 `revert` 한 결과,
어느 쪽 부모에 되돌릴지를 `-m`숫자로 지정합니다.숫자가 부모를 나타냅니다.

❖ 이 방법의 경우 취소한 Merge commit에 포함되어 있던 변경을
다시 Merge할 수 없게 됩니다.

> 예)
>- 브런치 A에 대하여 브런치 B를 마지
>- 머지(병합) 커밋을 revert하여 브랜치 A 상태로 되돌린다
>- 브랜치 A에 대하여 브랜치 B를 머지(병합)할 수 없음(변경이 받아들여지지 않음)

## 4. 머지(병합) 모두 완료했다. 근데 역시 되돌리고 싶을때. : case2
```
$ git reset --hard ORIG_HEAD
```
*머지(병합)하기 전*의 HEAD로 돌아갑니다.

❖ 이 방법은 한번 생긴 커밋을 `취소하는` 것입니다.
revert 명령과는 달리 '커밋을 취소했다'는 `이력도 남지 않습니다.`
일단 push 등을 수행하고 다른 개발자에게 공개된 커밋을 취소하는 것은 기본
절대 해서는 안 됩니다.

자신의 로컬만으로 머지(병합)해 보았지만 (push는 하지 않는 경우),
역시 그만두는 싶을 경우에만 사용해야 합니다.