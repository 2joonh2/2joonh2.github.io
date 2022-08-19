---
layout: single
title: "[Python] 이메일 송신"
categories: learn
toc: true
toc_sticky: true
---

Reference: ***열코***님의 [**파이썬으로 이메일 보내기(SMTP)**](https://yeolco.tistory.com/93)


```python
import smtplib
from email.mime.text import MIMEText

def sendmail(error=False):
    # 세션 생성
    s = smtplib.SMTP('smtp.gmail.com', 587)# TLS 보안 시작
    s.starttls()
    account_mail_address="2joonh2@gmail.com"

    f = open("C:/Users/2joon/OneDrive/문서/Gmail-app_pw.txt", 'r')
    pw = f.read()
    f.close()

    # 로그인 인증
    s.login(account_mail_address, pw)

    if error == False:     
        msg = MIMEText('The jupyter notebook has been completed.')
        msg['Subject'] = 'Execution Completed'
    else:
        msg = MIMEText('Error has occured, as below reason\n\n'+error)
        msg['Subject'] = 'Execution Failed'
    
    # 보낼 메시지 설정 - for 'try' successfuly being completed

    #메일 보내기
    s.sendmail(account_mail_address, "2joonh2@gmail.com", msg.as_string())
    # 세션 종료
    s.quit()
```

- 위 Cell의 세팅은 Reference 참조
- python으로 email를 보내는 기능을 구현하여, 소요시간이 오래걸리는 notebook에 try-exception과 결합하여 Execution 성공시 이메일을 보낼 수 있도록 함


```python
try:
    '''
    codes
    '''
    sendmail()
except Exception as ex:
    sendmail(str(ex))
```
