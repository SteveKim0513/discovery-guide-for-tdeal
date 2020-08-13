# Discovery 2.0 for T-Deal Guide Doc.
## URLs
Overlord Console : http://ec2-3-34-51-55.ap-northeast-2.compute.amazonaws.com:8090/console.html
Coordinator Console : http://ec2-3-34-51-55.ap-northeast-2.compute.amazonaws.com:8081/index.html#/
Airflow Console : http://ec2-3-34-51-55.ap-northeast-2.compute.amazonaws.com:8080/admin/

Discovery접속 URL : http://ec2-3-35-13-233.ap-northeast-2.compute.amazonaws.com:8180/app/v2/user/login


## 폴더 구조
/data/airflow : airflow가 설치된 폴더로 schduler를 만드는 파일이 있다.
> /data/airflow/app/

/data/


## ssh connection
```
$ ssh -i "Metatron.pem" ec2-user@ec2-3-34-51-55.ap-northeast-2.compute.amazonaws.com
$ sudo su metatron
```

## install python vm env.
```
$ cd /data/druid-ingestion/
$ python3 -m venv druid-batch
```

## druid ingestion test
1. enter python vm
```
$ . druid-batch/bin/activate
```

2. clone druid ingestion code from github(clone command at '/data/druid-ingestion/')
```
$ git clone https://github.com/SteveKim0513/t-deal-discovery.git
$ cd t-deal-discovery
$ pip install -r pip-requirements
```

3. change code in "~/t-deal-discovery/app/test.py"

4. execute python
```
$ python3 main.py --target {test}
```

5. Overlord Console Check


## make Data Schedule
*** create folder in S3 bucket ***
1. create folder in "metatron-druid-tdeal" bucket

2. make glue job

*** druid ingestion code ***
3. make ${dataName}.py in '/data/druid-ingestion/t-deal-discovery/app/'
> sample.py 복사하여 수정  
> 수정이 필요한 사항은 파일내에 주석으로 표기함

4. main.py 수정 in '/data/druid-ingestion/t-deal-discovery'
> 수정이 필요한 사항은 파일내에 주석으로 표기함

*** airflow conf. ***
5. enter airflow vm env.
```
$ source /data/airflow/venv/bin/activate
```

6. airflow 생성 파일 만들기: ${scheduleName}.py in '/data/airflow/dags'
> sample-airflow.py 복사하여 수정
> 수정이 필요한 사항은 파일내에 주석으로 표기함

7. airflow scheduler 등록
'''
$ airflow initdb
'''

8. airflow console에서 확인