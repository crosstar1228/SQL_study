### **1. 다음과 같은 스키마를 보고 student_info 테이블을 생성하는 명령어를 작성하라.**
![](https://images.velog.io/images/crosstar1228/post/335b900f-e237-41fa-84ff-f63d34e8ed28/image.png)

```sql
create table student_info(
stu_no char(10) not null,
stu_name char(10) not null,
sex char(2) not null,
birth_rate char(6) not null,
fee_enter int,
address varchar(100),
phone_no varchar(14),
primary key(stu_no)
);

desc student_info; # 스키마 확인
```
- varchar: 가변형 char형. 
- char : 정형 char형. 읽는 속도가 더 빠르다.

- not null : null을 허용하지 않음.


### **2. 1번에서 생성한 student_info 테이블에 다음 5개의 데이터를 삽입하는 명령어를 작성하고 student_info 테이블의 모든 데이터를 출력하라**
    
    (workbench 사용할 경우 여러 쿼리 실행시 **ctrl + shift+ enter**로 실행가능)
    
![](https://images.velog.io/images/crosstar1228/post/a32ea59e-8c7d-4af0-88aa-becf0e92743b/image.png)
```
insert into student_info values('20001001', '김유신', '남', '811007', 3000000, '마포', '011-617-1290')
insert into student_info values('20001001', '김유신', '남', '811007', 3000000, '마포', '011-617-1290');
insert into student_info values('20001015', '박도준', '남', '780116', 2500000, '양재', '011-611-9884');
insert into student_info values('20001021', '이상길', '남', '750819', null , '강남', null );

insert into student_info values('20041002', '김유미', '여', '830207', 1000000, '인천', '010-617-1290');
insert into student_info values('20041007', '정인정', '여', '830315', 2000000, '과천', '018-641-9304');

select * from student_info; # table 확인
```


### 3. student_info의 테이블의 null 값이 존재하는 데이터를 삭제하는 명령어를 작성하여라
    
    ```sql
    # Error Code: 1175 발생시 다음 코드 실행하고 삭제 진행
    set sql_safe_updates=0;
    delete from student_info where phone is null;

    
    
    
    ```
### 4. phone_no가 011으로 시작하는 데이터의 stu_no, stu_name, fee_enter을 조회하고 fee_enter 기준으로 오름차순 정렬하라.  
![](https://images.velog.io/images/crosstar1228/post/96750957-5171-44ba-8972-fae95eef6b5a/image.png)
```sql
    select stu_no, stu_name, fee_enter from student_info where phone_no like '011%' order by fee_enter asc;

```

### 5. fee_enter의 값이 2000000 이상 ~ 3000000 이하의 값을 가지는 데이터의 stu_name, fee_enter 를 조회하고 fee_enter는 숫자 3번째 자리마다 ,를 표시하라

```
select stu_name, format(fee_enter,'###,###') as formatted_fee_enter from student_info where fee_enter between 2000000 and 3000000;


```
![](https://images.velog.io/images/crosstar1228/post/bbef3801-56ef-4d1a-8505-8db3bdcd1021/image.png)


 ### 6. 성별을 기준으로 fee_enter의 총합을 구하고 다음과 같이 출력하라

```
select sex, sum(fee_enter) as sum_fee_enter from student_info group by sex;
```
![](https://images.velog.io/images/crosstar1228/post/b0853771-0a5b-495e-a41a-aa232bed4c93/image.png)

7.   성별을 기준으로 fee_enter의 최댓값을 구하라
```
select sex, max(fee_enter) as max_fee_enter from student_info group by sex;
```
![](https://images.velog.io/images/crosstar1228/post/e7a6f607-0a36-4d2e-82f8-f9691b0af1b3/image.png)


## 😎심화

### 8. 생년월일(birth_date)이 1980년 이후인 사람들의 fee_enter의 평균값을 조회하는 명령어를 작성하라.
 
```sql
select avg(fee_enter) from student_info where left(birth_rate, 2)>80;
```

![](https://images.velog.io/images/crosstar1228/post/b7075298-38a9-4c6f-9c8e-e6a4829b4ce3/image.png)




### 9. MySQL 사용시 테이블의 내용을 제거 하기 위한 명령으로 'DELETE' 와 'TRUNCATE' 가 있다.    
student_info의 모든 데이터를 삭제하고 delete와 truncate의 차이점을 설명하라.

```sql
# savepoint aa;

delete from student_info;
select * from student_info;

```
![](https://images.velog.io/images/crosstar1228/post/52abc97e-1640-49ed-bce4-e43f3fade9f1/image.png)

delete : rollback 명령어 통해 savepoint로 복구 가능
truncate : 불가능

(autocommit 해제해야 가능)
