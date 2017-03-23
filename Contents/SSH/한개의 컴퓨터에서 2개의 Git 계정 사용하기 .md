
## [ 한개의 컴퓨터에서 2개의 Git 계정 사용하기 ( SSH )]

GIt에 자료를 Push, Clone, Pull을 할 때 URL과 SSH를 사용할 수 있다. 나는 SSH와 URL방식 중 SSH를 사용하였다. 
SSH를 이용하여 1개의 계정만 사용할 때는 Push, Clone 등을 할 때 전혀 문제가 되지 않았다. 하지만 2개의 계정을 사용할 때 Error가 발생했다. 

	ERROR: Permission to charlesjeonewoo/Git.git denied to b08company.  
	fatal: Could not read from remote repository.
	
	Please make sure you have the correct access rights and the repository exists.

Permission관련 Error로 '이 계정에 다른 계정 ID로 접근할 수 없다'는 내용이었다. 


***계정 ID 맞추기***  

계정 아이디를 맞춰주기 위해 다음과 같이 하여 ID와 Email address를 맞추었다. 

	git config --global user.name "Username"  
	git config --global user.email "UserEmail Address"

하지만 같은 Error가 발생하였다.

	ERROR: Permission to charlesjeonewoo/Git.git denied to b08company.  
	fatal: Could not read from remote repository.
	
	Please make sure you have the correct access rights and the repository exists.

Username을 설정하는 것으로는 Error가 해결되지 않았다.


***Github에 SSH추가 하기***  


_SSH 생성하기_

Github에 SSH를 추가 하기 위해서는 먼저 PC에서 SSH를 만들어야 한다. 만드는 방법은 다음을 Command창에 치면 된다. 

	ssh-keygen -t rsa -C "User email"

그러면 다음과 같이 Directory, password를 입력하도록 나온다. 

	Generating public/private rsa key pair.
	Enter file in which to save the key (/Users/GANDIS/.ssh/id_rsa): 

경로는 .ssh폴더에 작성해야 한다. id_rsa는 SSH filename으로 본인이 원하는 것으로 바꾸어도 된다. SSH filename까지 완료하면 다음과 같이 password를 입력하라고 나온다. 
	
	Enter passphrase (empty for no passphrase): 
	Enter same passphrase again: 

password까지 모두 완료하고 나면 다음과 같이 SSH 생성이 완료 된다.

	Your identification has been saved in /Users/GANDIS/.ssh/test.
	Your public key has been saved in /Users/GANDIS/.ssh/test.pub.
	The key fingerprint is:
	SHA256:MYMzik6NJgt6v84l8HiIWMS5dOvJjWEsYsPNjFn0VNQ test@naver.com
	The key's randomart image is:
	+---[RSA 2048]----+
	|   . .oo.        |
	| ...o  . E       |
	|  =...+ +        |
	|.oBB o o +       |
	|+*X+B   S        |
	|=X.X =           |
	|= = O o          |
	| . + o           |
	|   .=.           |
	+----[SHA256]-----+

_SSH 추가하기_

Github에 로그인 후 아래 그림의 상단 메뉴에서 _Setting_을 선택한다.    

![](https://github.com/charlesjeonewoo/Git/blob/master/Resouce/Add_SSH_1.png)

왼쪽 상단 메뉴에서 _SSH and GPG keys_를 선택한다.  

![](https://github.com/charlesjeonewoo/Git/blob/master/Resouce/Add_SSH_2.png)

New SSH key를 눌러 생성한 SSH를 추가한다.  

![](https://github.com/charlesjeonewoo/Git/blob/master/Resouce/Add_SSH_3.png)

Github에 SSH까지 추가를 하고 다시 Push를 시도해보았다. 하지만

	ERROR: Permission to charlesjeonewoo/Git.git denied to b08company.  
	fatal: Could not read from remote repository.
	
	Please make sure you have the correct access rights and the repository exists.

똑같은 Error가 발생하였다. Google 검색결과 

	ssh-add ~/.ssh/b08company

로 사용하고자 하는 public SSH를 추가하라는 것 같다. 결과는 성공!

하지만 다른 아이디인 charlesewoojeon로 push를 하려고 하니 이번에는 반대로 

	ERROR: Permission to b08compnay/RevengiDidt.git denied to charlesjeonewoo.  
	fatal: Could not read from remote repository.
	
	Please make sure you have the correct access rights and the repository exists.

Error가 발생했다. 그래서 Google 검색 결과 대로 
 
	ssh-add ~/.ssh/charlesjeonewoo

으로 해당 사용자의 public SSH를 추가했다. 결과는 

	ERROR: Permission to b08compnay/RevengiDidt.git denied to charlesjeonewoo.  
	fatal: Could not read from remote repository.
	
	Please make sure you have the correct access rights and the repository exists.

실패! 이유는 모르겠다.

	ssh-add -l

위의 명령어 입력 결과 두 계정의 public SSH가 모두 추가 되었다. 

	ssh-add -D
	ssh-add ~/.ssh/charlesjeonewoo

추가된 SSH를 모두 지우고 다시 추가를 해보았다. 
결과는 성공이었다. 
매번 이렇게 모두 지우고 다시 추가를 반복해야 된다. Google 검색을 다시 했다.
아래와 같이 .ssh/config 파일을 수정하고, remote할 SSH를 바꾸어 주면 되었다.

	vi ~/.ssh/config

를 입력해 config 파일을 연다. 그리고 다음과 같이 수정한다.

	# b08company Account
	# Email : b08company@naver.com

	Host github.com-b08company
        HostName github.com
        User git
        IdentityFile ~/.ssh/b08company


	# charlesjeonewoo Account
	# Email : charlesjeon.ewoo@gmail.com

	Host github.com-charlesjeonewoo
        HostName github.com
        User git
        IdentityFile ~/.ssh/charlesjeonewoo

config 파일 수정이 완료 되면 GitHub에서 제공하는 SSH주소를 다음과 같이 변경하여 remote한다.

	git@github.com:charlesjeonewoo/Git.git  // 기존주소
    git@github.com-charlesjeonewoo:charlesjeonewoo/Git.git  // 변경주소

그리고 나면 두 계정의 SSH를 등록했다 지원다 하지 않고, 자유롭게 push를 할 수 있다. 

---
### URL

URL을 사용하면 SSH와 달리 Github에 SSH를 등록할 필요가 없다. 다만 다음과 같이 Github에 접속할 때 Username과 Password를 사용하면 된다.

	Username for 'https://github.com': charlesjeon.ewoo@gmail.com
	Password for 'https://charlesjeon.ewoo@gmail.com@github.com':


