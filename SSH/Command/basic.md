**SSH 파일 경로 이동**

	cd ~/.ssh

**SSH file list 확인**

    ls -al ~/.ssh

**SSH 만들기**

	ssh-keygen -t rsa -C "Username@gmail.com"

**SSH 열기**

	cat "SSH file"

**SSH 추가**

	ssh-add "SSH file"

**추가된 SSH 삭제**

	ssh-add -d "SSH file"  //추가된 SSH 파일 1개 삭제
	ssh-add -D             //추가된 SSH 파일 모두 삭제
