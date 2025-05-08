## GCP 환경에서 CI/CD 파이프라인 구축하기

ubuntu 환경에서 젠킨스 설치

1. 자바 설치
```
sudo apt install openjdk-17-jdk
```

2. 리포지토리 등록
```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

3. update후 젠킨스 설치
```
sudo apt update

sudo apt install jenkins
```

4. 기본 8080포트에서 9090포트로 변경
```
sudo vi /etc/default/jenkins

HTTP_PORT=9090
```

```
sudo vi /etc/init.d/jenkins

check_top_port=... "9090" ...
```

```
sudo vi /lib/systemd/system/jenkins.service

Environment="JENKINS_PORT=9090"
```

5. 변경 후 젠킨스 재시작
```
sudo systemctl stop jenkins
sudo systemctl daemon-reload
sudo systemctl start jenkins
```
