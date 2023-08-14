# Ubuntu 22.04 초기 설정
## 초기 설정
- Wifi 설정하기 : ID, Passwd
- 시스템 업데이트 (첫 부팅)
```bash
    sudo apt update
    sudo apt upgrade
```
- 설치
```bash
    sudo apt install git  
    sudo apt install net-tools # ifconfg  명령 사용 가능
```
- ssh 설치
```bash
    sudo apt install openssh-server
```
- 시스템 restart
```bash    
    sudo systemctl status ssh  # SSH 서버 실행 중인지 상태 확인
    sudo systemctl start ssh # SSH 서버가 실행시키기 
    sudo ufw allow 22
    sudo ufw allow ssh
    sudo ufw status
    sudo ufw enable
    sudo systemctl restart ssh
```
- 시스템 restart

- 카메라 interface 사용하게 해주는 설정 어플 설치하기
```bash
    sudo apt install raspi-config
```
