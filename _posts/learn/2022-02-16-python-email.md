---
layout: single
title: "[Python] 이메일 송신"
categories: learn
toc: true
---

Reference: ***열코***님의 [**파이썬으로 이메일 보내기(SMTP)**](https://yeolco.tistory.com/93)


```python
import smtplib
from email.mime.text import MIMEText
```


```python
# 세션 생성
s = smtplib.SMTP('smtp.gmail.com', 587)# TLS 보안 시작
s.starttls()
```




    (220, b'2.0.0 Ready to start TLS')




```python
account_mail_address="2joonh2@gmail.com"

f = open("C:\\Users\\2joon\\OneDrive\\문서\\Gmail-app_pw.txt", 'r')
pw = f.read()
f.close()

# 로그인 인증
s.login(account_mail_address, pw)
```




    (235, b'2.7.0 Accepted')




```python
# 보낼 메시지 설정 - 1) try codes complete
msg_t= MIMEText('The jupyter notebook has been completed.')
msg_t['Subject'] = 'Execution Completed'
```


```python
# 보낼 메시지 설정 - 2) except codes; errors occur
msg_f= MIMEText('An error has occured, the notebook send the message for alert.')
msg_f['Subject'] = 'Execution Failed'
```


```python
#메일 보내기
s.sendmail(account_mail_address, "2joonh2@kaist.ac.kr", msg_t.as_string())

# 세션 종료
s.quit()
```




    (221, b'2.0.0 closing connection k11sm2209552pfu.150 - gsmtp')

