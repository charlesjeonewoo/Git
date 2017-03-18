
### [ 한개의 컴퓨터에서 2개의 Git 계정 사용하기 ]

GIt에 Push, Clone, Pull을 할 때 URL과 SSH를 사용할 수 있다. 나는 SSH를 몰랐기 때문에 URL을 사용하였다.  
1개의 계정만 사용할 때는 Push, Clone 등을 할 때 전혀 문제가 되지 않았다. 하지만 2개의 계정을 사용할 때 Error가 발생했다. Permission관련 Error로 '이 계정에 다른 계정 ID로 접근할 수 없다'는 내용이었다. 

나는 이 Error를 해결하기 위해 여러가지를 해보았다. 
아래는 내가 그 동안 해 보았던 내용을 정리하였다.    

***계정 ID 맞추기***  

계정 아이디를 맞춰주기 위해 다음과 같이 하여 ID와 Email address를 맞추었다. 

	git config --global user.name "Username"  
	git config --global user.email "UserEmail Address"

하지만 다음과 같은 Error가 발생하였다.

	ERROR: Permission to "Username"/"Repository".git denied to "Other Username".  
	fatal: Could not read from remote repository.
	
	Please make sure you have the correct access rights and the repository exists.

Username을 설정하는 것으로는 Error가 해결되지 않았다.


***SSH 사용하기***  
