# First

##  2017년 9월 2일
## code
```python
# _*_ coding: utf-8 _*_     #한글과 같은 ascii 이외의 characterset을 처리하기 위해서
from flask import Flask     #flask class 를 임포트 했다

app = Flask(__name__)       #instance를 생성 한다. / __name__은 이 프로젝트의 이름 이다.

@app.route("/hello/")       #routing 해주는 것 이다.
def hello():
return "hello world!!"

if __name__=="__main__":
app.debug = True	    #내용이 변환이 된다면 스스로 재시작을 한다.
app.run()               #실행을 한다.
```
----------------------------

# second

## 2017년 9월 4일
## code
+ url 패턴 변수 처리
```python
#_*_coding: utf-8_*_
from flask import Flask

app = Flask(__name__)

@app.route("/profile/<username>")   #url패턴을 변수로 처리가 가능하다

def showProfile(username):          #컨트롤러 설정
    return "USER : %s" % username

@app.route("/post/<int:post_id>")   #인자를 정수형으로만 입력을 받을 수 있도록 할 수 있다.
def showPost(post_id):
    return "Post_id : %d" % post_id

if __name__=="__main__":            #내장 서버 실행
    app.debug = True
    app.run()
```

+ logging
```python
#_*_coding: utf-8_*_

from flask import Flask

app = Flask(__name__)

@app.route("/logging")              #logging이라는 위치로 라우팅
def showLogging():                  #이 함수를 사용하면 console으로만 나타남 자신이 원하는 결과를 띄울 수 있음
    test = 1
    app.logger.debug("디버깅 필요")
    app.logger.warning(str(test) + " 라인")
    app.logger.error("에러 발생")
    return "로깅 끝"

if __name__=="__main__":
    app.debug = True
    app.run()
```
-------------
# third

## 2017년 9월 5일
## code
```python
#_*_coding: utf-8_*_
from flask import Flask, render_template, request, session

app = Flask(__name__)

@app.route("/login_form")
def login_from():
    return render_template("login_form.html")   #login_form.html로 넘어간다.

@app.route("/login", methods=['POST'])      #post방식으로 보내겠다를 정함.
def login():
    if request.method == 'POST':
        if request.form['username'] == 'kang' and request.form['password'] == '1234':       #post방식에서 받는 방법
            session['logged_in'] = True
            session['username'] = request.form['username']
            return request.form['username'] + " 님 환영합니다.".decode('utf-8')
        else:
            return "로그인 정보가 맞지 않습니다."
    else:
        return "잘못된 접근 입니다."
app.secret_key = 'sample_secret_key'    #session key값을 추가 해준 것이다.

if __name__=="__main__":
    app.debug = True
    app.run()
```