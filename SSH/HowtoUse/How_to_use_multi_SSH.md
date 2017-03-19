
## [ 한개의 컴퓨터에서 2개의 Git 계정 사용하기 ( SSH )]

GIt에 자료를 Push, Clone, Pull을 할 때 URL과 SSH를 사용할 수 있다. 나는 SSH를 몰랐기 때문에 URL을 사용하였다. 하지만 지금은 SSH를 이용한다.
SSH를 이용하여 1개의 계정만 사용할 때는 Push, Clone 등을 할 때 전혀 문제가 되지 않았다. 하지만 2개의 계정을 사용할 때 Error가 발생했다. Permission관련 Error로 '이 계정에 다른 계정 ID로 접근할 수 없다'는 내용이었다. 

나는 이 Error를 해결하기 위해 여러가지를 해보았다. 
아래는 내가 그 동안 해 보았던 내용을 SSH와 URL로 나누어서 정리하였다.


---
### SSH

***계정 ID 맞추기***  

계정 아이디를 맞춰주기 위해 다음과 같이 하여 ID와 Email address를 맞추었다. 

	git config --global user.name "Username"  
	git config --global user.email "UserEmail Address"

하지만 다음과 같은 Error가 발생하였다.

	ERROR: Permission to "Username"/"Repository".git denied to "Other Username".  
	fatal: Could not read from remote repository.
	
	Please make sure you have the correct access rights and the repository exists.

Username을 설정하는 것으로는 Error가 해결되지 않았다.


***Github에 SSH추가 하기***  


_SSH 생성하기_

Github에 SSH를 추가 하기 위해서는 먼저 PC에서 SSH를 만들어야 한다. 만드는 방법은 다음을 Command창에 치면 된다. 

	ssh-keygen -t rsa -C "User email"

그리고 다음과 같이 Directory, password를 입력하도록 나온다. 

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

![image1] (https://github.com/charlesjeonewoo/Git/blob/master/Resouce/Add_SSH_1.png)

왼쪽 상단 메뉴에서 _SSH and GPG keys_를 선택한다.  

![] (https://github.com/charlesjeonewoo/Git/blob/master/Resouce/Add_SSH_2.png)

New SSH key를 눌러 생성한 SSH를 추가한다.  

![] (https://github.com/charlesjeonewoo/Git/blob/master/Resouce/Add_SSH_3.png)


---
### URL

URL을 사용하면 SSH와 달리 Github에 SSH를 등록할 필요가 없다. 다만 다음과 같이 Github에 접속할 때 Username과 Password를 사용하면 된다.

	Username for 'https://github.com': charlesjeon.ewoo@gmail.com
	Password for 'https://charlesjeon.ewoo@gmail.com@github.com':

___

SSH를 사용하는 이유와 장점은 모르겠다. 확인해보고 이부분에 대해서 update할 예정이다.