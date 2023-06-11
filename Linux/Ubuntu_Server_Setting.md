### 서버 접속
> ssh -i mysite.pem ubuntu@[ip주소]

### hostname변경
> <span style="color:gray;"> //hostname jumpto로 변경 </span><br/>
> ubuntu@<span style="color:yellow;">ip-111-21-0-39</span>:~$ hostnamectl set-hostname jumpto <hostname> <br/>
> <span style="color:gray;"> //서버 리스타트 </span> <br/>
> ubuntu@<span style="color:yellow;">ip-111-21-0-39</span>:~$ sudo reboot <br/>
> <span style="color:gray;"> //hostname 변경 확인 </span> <br/>
> ubuntu@<span style="color:yellow;">jumpto</span>:~$

### 서버 시간 설정
AWS 서버의 기본 시간은 UTC 국제 표준 시간이므로 우리나라 시간으로 변경
> ubuntu@jumpto:~$ sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime

### 패키지 업데이트
> ubuntu@jumpto:~$ sudo apt-get update

### 자바 설치
> ubuntu@jumpto:~$ sudo apt-get install openjdk-17-jdk



### MySQL 설치
> ubuntu@jumpto:~$ sudo apt-get install mysql-server
> 
> ubuntu@jumpto:~$ sudo mysql --version

AWS Lightsail 서버에서 MySQL 접속
> mysql -h 엔드포인트 -P 포트 -u 사용자명 -p

### MySQL 한글 설정
> mysql> show variables like 'c%';