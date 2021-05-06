## Git
git config --list
git config --global -e
git config --global core.editor "code"
And git config --global -

git config --global core.editor ""code --wait"
And git config --global -e

## Set User detail
git config --global user.name "jake"
git config --global user.email "jakethechanger@gmail.com"
git config user.name
git config user.email

## windows \r\n, mac \n
git config --global core.autocrlf input


## git command -option

## git init
깃의 초기화
기본적으로 master branch가 생성

open .git
rm -rf .git

## sourcetree
초기화된 깃 폴더를 드래그

## git config --global alias
git config --global.st status
git st

## git config --h
속성값, 명령어 확인


## git 작업환경 workflow
1. working directory (수정, 작업하고 있는 디렉토리)
git add (untracked to tracked)
2. staging area (버전 히스토리에 저장할 준비가 되어있는 파일들을 옮겨놓는 스테이징 영역)
git commit (to staging)
3. .git directory (버전의 히스토리를 가지고 있는 git repository 또는 git directory)
*** git checkout 원하는 버전으로 돌아갈수 있음

4. git remote server .git directory
git push - git 서버에 업로드
git pull - 로컬로 다시 다운로드


## file status
Working directory는 2개로 나뉨
untracked v tracked (unmodified v modified) 그래서 modified 된 tracked file만 staging으로 옮겨갈수 있다.

## 실습

echo Hello World! > a.txt
echo Hello World! > b.txt
echo Hello World! > c.txt

git status

***
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	a.txt
	b.txt
	c.txt
***

git add a.txt

***
No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   a.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	b.txt
	c.txt
***

git add *.txt (or git add b.txt c.txt)

***
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   a.txt
	new file:   b.txt
	new file:   c.txt
***

커밋전에 파일 수정이 있다면?
echo Jake >> a.txt

***
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   a.txt
	new file:   b.txt
	new file:   c.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   a.txt
***

git add a.txt
수정된 부분 포함 staging으로 올라감
git rm -cached <file>을 통해 unstage로 돌아갈수 있음 (untracked status)

***
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   a.txt
	new file:   b.txt
	new file:   c.txt
***

git rm --cached *.txt

***
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	a.txt
	b.txt
	c.txt

nothing added to commit but untracked files present (use "git add" to track)
***

만약 staging으로 옮기고 삭제가 되다면
git add *
rm a.txt
git status
***
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   a.txt
	new file:   b.txt
	new file:   c.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    a.txt
***

삭제된것이 적용
git add .
git status

***
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   b.txt
	new file:   c.txt
***

Tracking, uploading하고 싶지 않은 파일
echo *.log > .gitignore

***

***
echo log.log > .gitignore
echo *.log > .gitignore
echo folder/ > .gitignore
echo folder/*.log > .gitignore
***

git status -s
***
AM b.txt
A  c.txt
?? .gitignore
***

git diff(working directory에 있는 변경사항만 확인)

diff --git a/b.txt b/b.txt
index 980a0d5..be36e6e 100644
--- a/b.txt
+++ b/b.txt
@@ -1 +1,2 @@
 Hello World!
+add

git diff --staged === git diff --cached
***
diff --git a/b.txt b/b.txt
new file mode 100644
index 0000000..980a0d5
--- /dev/null
+++ b/b.txt
@@ -0,0 +1 @@
+Hello World!
diff --git a/c.txt b/c.txt
new file mode 100644
index 0000000..980a0d5
--- /dev/null
+++ b/c.txt
@@ -0,0 +1 @@
+Hello World!
(END)
***


변경사항을 에디터에서 확인하고 싶다면

git config --global -e

[diff]
tool = vscode

[difftool "vscode"]
cmd = code --wait --diff $LOCAL $REMOTE

git difftool
git difftool -staged


## commit으로 버전 생성
git commit
***
michaelflynn@Michaels-MacBook-Air  ~/Desktop/test/gitStudy/git   master ±✚  git commit
[master (root-commit) 5826089] Title
 2 files changed, 2 insertions(+)
 create mode 100644 b.txt
 create mode 100644 c.txt
***

git log
***
Author: jake <jakethechanger@gmail.com>
Date:   Mon May 3 23:01:42 2021 +0700

    Title

    Description
***


git commit -m "2nd commit"
***
[master c03e377] 2nd commit
 2 files changed, 3 insertions(+)
 ***

 git log
 ***
 Author: jake <jakethechanger@gmail.com>
Date:   Mon May 3 23:04:51 2021 +0700

    2nd commit

commit 58260898a445b0390f1e297a03849cdba1e13308
Author: jake <jakethechanger@gmail.com>
Date:   Mon May 3 23:01:42 2021 +0700

    Title

    Description
***


Git test