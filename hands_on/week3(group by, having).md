## Configuration

> database에 haksa_db 를 추가하고, dump.sql 에 해당하는 파일을 import한 후 실습 진행

[dump.sql 다운로드](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e3faadd8-2b5d-46e0-ad12-3bb9fb875b07/dump.sql?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20211122%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211122T060459Z&X-Amz-Expires=86400&X-Amz-Signature=e2cbe455796d63ba68217b20e8845db51fb60de69b86798666d63fd8cff76a3d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22dump.sql%22&x-id=GetObject)
(우클릭 후 다른 이름으로 링크 저장)

```
show databases;
create database haksa_db;
use haksa_db;
## dump.sql import 후
show tables;
```
![](https://images.velog.io/images/crosstar1228/post/9e92a886-74ce-4ffc-9c2a-c54a21307e40/image.png)

## 1. 2개 열에 대한 그룹화
### student table 확인
```
select * from student;
```
![](https://images.velog.io/images/crosstar1228/post/9297ef26-81d4-46e1-80c1-3044f06a4af1/image.png)


1. student 테이블에 있는 학생의 학년(grade)별 그룹과 인원을 출력하고 학년(grade)을 기준으로 정렬하라
```
select grade as 학년, count(stu_no) as 인원 from student group by grade order by grade asc;
```
![](https://images.velog.io/images/crosstar1228/post/e575d905-746a-4e7b-bab9-06514e2a3c4d/image.png)

2. 각 입학년도별 총 학생 수를 출력하라

```
select left(stu_no,4) as 입학년도, count(stu_no) as 인원 from student group by  left(stu_no,4) order by left(stu_no,4);
```
![](https://images.velog.io/images/crosstar1228/post/c776f93c-b9b0-4323-bc5a-37e492b5173b/image.png)



### fee table 확인

![](https://images.velog.io/images/crosstar1228/post/e4efad2b-eab2-441a-8ef7-5aa527814d63/image.png)

3. fee 테이블로부터 등록년도(fee_year)에 대하여 등록횟수를 출력하라.
```
select fee_year as 등록년도, count(fee_year) as 등록횟수 from fee
group by fee_year
order by fee_year asc;
```
![](https://images.velog.io/images/crosstar1228/post/025bea79-b5b0-4b2e-8975-c47780e887bc/image.png)

4. fee 테이블에서 **학번을 기준**으로  **학번**, **등록횟수**, **각 학생이 받은 장학금의 전체 합**을 출력하라

```
select stu_no as 학번,
count(stu_no) as 등록횟수,
sum(jang_total) as 장학금총합
from fee
group by stu_no
order by stu_no asc;
```
![](https://images.velog.io/images/crosstar1228/post/47499278-59ec-465e-8e4d-819beeb51849/image.png)

5. 박정인 학생에 대하여 학번,  등록횟수를 출력하라 (fee, student 테이블 사용, 서브쿼리 사용)

```
select stu_no as 학번, count(stu_no) as 등록횟수 from fee
where stu_no in (select stu_no from student where stu_name = ('박정인'));
```
![](https://images.velog.io/images/crosstar1228/post/653ca413-f175-4f68-bcae-7ffe14d3e91d/image.png)


## 3개 이상의 열에 대한 그룹화

1. student 테이블로부터 학년(grade)별, 주야(juya)별 인원수를 출력하라. 단 출력 순서는 학년별 오름차순, 주야 오름차순이다.
![](https://images.velog.io/images/crosstar1228/post/ab831d9c-9308-4b7c-8b3a-32714e750eb9/image.png)

2. student 테이블로부터  학년(grade), 반(class), 주야(juya)구분이 서로 다른 모든 조합을 인원수로 출력하라. 단 출력 순서는 학년별 오름차순이다.

```
#해당 모든 칼럼을 group by 에 넣는다!
select grade, class, juya from student group by grade, class, juya order by grade asc;

```

![](https://images.velog.io/images/crosstar1228/post/1e2df504-856d-4984-9f9c-37f2da03c038/image.png)

3. **fee 테이블로부터 각 학생별로 대학 재학시 납입금(fee_pay) 총액과 등록금(fee_total) 최대값, 가장 적게 받은 장학금(jang_total), 등록 횟수를 출력하라.**

```
select stu_no, sum(fee_pay), max(fee_total), min(jang_total), count(stu_no) from fee group by stu_no order by stu_no;
```
![](https://images.velog.io/images/crosstar1228/post/706e8433-f60f-4790-af75-bba4b4a80e32/image.png)


4. **등록한 학생에 대하여 학번, 이름, 납입금(fee_pay) 총액을 출력하라. (이름 정보는 student 테이블에 존재한다)**

```
## 각 table별로 멀티select, 그리고 where 문 활용
select student.stu_no, stu_name, sum(fee.fee_pay) from student, fee where student.stu_no = fee.stu_no group by student.stu_no, stu_name;
```

![](https://images.velog.io/images/crosstar1228/post/df65cc0b-f520-41b5-bc9c-6ba2868757da/image.png)



## 3. Null 값의 그룹화 : isnull()
- NULL 값을 가지고 있는 열을 group by하면 NULL 값은 하나의 그룹으로 구성된다.

1. fee 테이블로부터 서로 다른 장학코드(jang_code)를 그룹화하고 인원수를 출력하라. 단 jang_code의 값이 null인 경우 null로 표시하라

```
select ifnull(jang_code,null), count(jang_code) from fee group by jang_code;
```
![](https://images.velog.io/images/crosstar1228/post/f2174420-378a-4eb3-833b-9dd67dbe9a80/image.png)

## 4. Having!
- `GROUP BY` 통해 그룹화된 그룹에 대한 조건문 설정(마치 where 처럼)

2. fee 테이블로부터 세 번 이상 등록한 학생의 학번과 등록 횟수를 출력하라
```
select stu_no, count(stu_no) from fee group by stu_no having count(stu_no)>3;
```

![](https://images.velog.io/images/crosstar1228/post/b11893b4-b9f9-4278-b1be-6b207efc85d4/image.png)





3. fee 테이블로부터 2006년에 등록한 학생의 학번과 등록 횟수를 출력하라.

```
select stu_no, fee_year, count(stu_no) from fee group by stu_no,fee_year having fee_year = '2006';
```
> group by에 두 칼럼을 추가해야 오류가 안나네. 왤까?


![](https://images.velog.io/images/crosstar1228/post/d2196308-a6f9-4389-8c1b-31c52197430a/image.png)


4. fee 테이블로부터 납입금(fee_pay)의 총액이 5,000,000원 이상인 각 학생에 대하여 출력하라

```
select stu_no, sum(fee_pay) from fee group by stu_no having sum(fee_pay) > 5000000;
```

![](https://images.velog.io/images/crosstar1228/post/137bd5df-07cc-44c2-ab65-b488f10ba014/image.png)