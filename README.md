# pymysql

## 기본 문법
```
import pymysql
conn = pymysql.connect(host="202.30.16.152", user="root", password="tksgkrdnjs1", db="{#데이터베이스 이름}", charset='utf8')

# Connection 으로부터 Cursor 생성
curs = conn.cursor()

# SQL문 실행종류
sql = "{#SQL 문법, 세미콜론 제외}"
curs.execute(sql)

# 데이타 Fetch
rows = curs.fetchall()

print(rows)

# Connection 닫기
conn.close()
```

# 클래스
```
class SQLClass:

    def __init__(self, host, user, pw, db):
        self.host = host
        self.user = user
        self.pw = pw
        self.db = db


    def processing(self):
        # Reference
        # https://velog.io/@new_wisdom/Python-Mysql-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-insert
        # http://pythonstudy.xyz/python/article/202-MySQL-%EC%BF%BC%EB%A6%AC

        import pymysql

        conn = pymysql.connect(host=self.host, user=self.user,
                               password=self.pw,
                               db=self.db, charset='utf8')

        # Connection 으로부터 Cursor 생성
        curs = conn.cursor(pymysql.cursors.DictCursor)

        # SQL문 실행종류
        sql = "{#SQL 문법, 세미콜론 제외}"
        curs.execute(sql)

        # 데이타 Fetch
        rows = curs.fetchall()

        # Connection 닫기
        conn.close()

        return rows
```
## 사용
```
from {#클래스 경로} import SQLClass

# MySQL 서버 연결
connectSQL = SQLClass("202.30.16.152", "root", "tksgkrdnjs1", "{#데이터베이스 이름}")

# 실행
excuteClass = connectSQL.processing()

# 출력
print(excuteClass)
```

## 데이터 업데이트
```
class InsertInfo:

    def __init__(self, host, user, pw, db):
        self.host = host
        self.user = user
        self.pw = pw
        self.db = db


    def processing(self):
        # Reference
        # https://velog.io/@new_wisdom/Python-Mysql-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-insert
        # http://pythonstudy.xyz/python/article/202-MySQL-%EC%BF%BC%EB%A6%AC
        import pandas as pd

        path = '{# 엑실, csv 등의 데이터 경로}'
        df = pd.read_excel(path, engine='openpyxl')
        for idx, row in df.iterrows():

            import pymysql

            conn = pymysql.connect(host=self.host, user=self.user,
                                   password=self.pw,
                                   db=self.db, charset='utf8')

            # Connection 으로부터 Cursor 생성
            curs = conn.cursor(pymysql.cursors.DictCursor)

            # SQL문 실행종류
            sql = "INSERT into {#테이블명} (nobleDiv, dep, region, belong_1, belong_2, nobleCls, name, hanjaname, memo, source) VALUES (%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"
            
            # 데이터프레임의 행을 한 줄씩 INSERT하는 작업
            val = (str(row['문반-서반']), str(row['종류']), str(row['지역']), str(row['소속(1)']), str(row['소속(2)']), str(row['품계']),str(row['관직(한글)']), str(row['관직(한자)']), str(row['비고(2)']), str(row['출처']))
            curs.execute(sql, val)
            conn.commit()


```
