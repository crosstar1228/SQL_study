> [지난 groupby 실습](https://velog.io/@crosstar1228/SQLGROUP-BY%EC%97%B4-2%EA%B0%9C-%EC%97%B4-3%EA%B0%9C-null%EA%B0%92-%EC%B2%98%EB%A6%AC%EC%99%80-having-%ED%99%9C%EC%9A%A9) 에서 사용된 haksa_db 데이터베이스를 이용해서 실습이 진행됩니다.

## JOIN이란

- 두 테이블 연결 또는 결합하여 데이터 출력
- 일반적인 경우 PRIMARY KEY(PK) 나 FOREIGN KEY(FK) 값의 연관에 의해 JOIN이 성립

![](https://images.velog.io/images/crosstar1228/post/c7c4d1aa-0057-47d0-b038-a7ed985b8f2a/image.png)
[https://opentutorials.org/course/195/1409]


**1. INNER JOIN : 겹치는 값만 선택! 데이터가 없는 쪽에 맞춘다.**
**2. OUTER JOIN : 한쪽에는 있고, 한쪽에는 없는경우, 데이터가 있는 쪽에 맞춘다.**

	- LEFT OUTER JOIN : A를 기준으로 B도 가져옴. B 테이블에 A 테이블과 같은 값이 없으면 NULL로 채워 반환
	- RIGHT OUTER JOIN : 반대
	- FULL OUTER JOIN : 두 테이블 모든 값을 반환한다. 중복되는 데이터는 삭제한다. 
    
## JOIN의 종류
### 1. CROSS JOIN (where 활용되기도)
- 가장 간단한 방법
- 통합된 모든 행을 출력하고 중복되는 행은 제거
- 모든 행을 가져오기 때문에 정규화된 DB에서는 사용 잘 안함

- 반환 행 수 : (A table 행 수) * (B table 행 수)

1) student 테이블과 score 테이블을 cross join 하여 stu_no, stu_name , sco_year , sco_term 을 출력하라.

```sql
select s.stu_no, s.stu_name, sc.sco_year, sc.sco_term from student s inner join score sc;

## 또는!
select s.stu_no, s.stu_name, sc.sco_year, sc.sco_term from student s, score sc;

```
![](https://images.velog.io/images/crosstar1228/post/4f17fd31-d57b-4f71-a09e-b694a45ddb32/image.png)


2) student 테이블과 score 테이블을 cross join 하여 stu_no, stu_name, sco_year, sco_term 을 출력하라. (단, student 테이블에 존재하는 "20061011" 학생만을 출력하라)

```sql
## on, inner join 사용
select s.stu_no, s.stu_name, sc.sco_year, sc.sco_term from student s inner join score sc **on** s.stu_no = '20061011';

## where, inner join 사용
select s.stu_no, s.stu_name, sc.sco_year, sc.sco_term from student s inner join score sc **where** s.stu_no = '20061011';

## where 만 사용
select s.stu_no, s.stu_name, sc.sco_year, sc.sco_term from student s, score sc where s.stu_no = '20061011';

```
![](https://images.velog.io/images/crosstar1228/post/f465a77a-413b-4ff2-949d-6e28eb6aa626/image.png)



### WHERE VS ON
- ON : JOIN 을 하기 전 필터링을 한다 (=ON 조건으로 필터링이 된 레코들간 JOIN이 이뤄진다)
- WHERE : JOIN 을 한 후 필터링을 한다 (=JOIN을 한 결과에서 WHERE 조건절로 필터링이 이뤄진다)

### 2. Equal join : where {}={} and {}={} ...
1) student 테이블에 존재하는 학생들 중에서 등록한 학생의 학번(stu_no), 이름(stu_name), 반(class), 등록년도(fee_year), 학기(fee_term), 등록금 총액(fee_pay)를 출력하라.

```sql
select s.stu_no, s.stu_name, s.class, f.fee_year, f.fee_term, f.fee_pay from student s, fee f where s.stu_no=f.stu_no; 
```
![](https://images.velog.io/images/crosstar1228/post/c9cb8a69-28f9-4d14-b21c-401633ffcd08/image.png)

> WHERE절의 조건 연산자가 = 인 경우에 FROM 절에 나오는 STUDENT 테이블의 모집단이 FEE 테이블의 모집단을 전부 포함하고 있다면 INNER EQUI JOIN 이라고 한다. 만약 FEE 테이블의 모집단이 STUDENT 의 모집단을 포함하고 있다면 OUTER EQUI JOIN 이라고 한다.

2. 재학생이면서 attend테이블에 존재하는 학생의 학번(stu_no), 이름(stu_name), 수강신청년도(att_year),  학기(att_term), 과목코드(sub_code), 과목명(sub_name), 교수코드(prof_code), 교수명(prof_name) 를 출력하라. ( 출력 순서는 학번, 수강년도, 수강학기, 수강코드순이다.)

```sql
select s.stu_no, s.stu_name, a.att_year,a.att_term, a.sub_code, su.sub_name, a.prof_code, p.prof_name
from student s, attend a, subject su, professor p
where s.stu_no=a.stu_no and a.sub_code=su.sub_code and a.prof_code=p.prof_code
order by s.stu_no, a.att_year, a.att_term, a.sub_code; 
```
![](https://images.velog.io/images/crosstar1228/post/9d9603cc-5f75-4fe0-8d33-e477ce0f317b/image.png)



> 다음 시간에는 **OUTER JOIN과 그 명령어를 활용힌 실습**을 진행해 볼게요!



