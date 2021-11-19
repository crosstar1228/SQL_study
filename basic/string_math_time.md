> 문자나 숫자를 디테일하게 다뤄 봅시다.

## length : 길이 측정
```
select length('abcde');
```
![](https://images.velog.io/images/crosstar1228/post/0b9d2f20-ca45-4ab6-92c0-d382f7a50029/image.png)
## 문자 연결 : concat

```
select concat('a','b','c');
```
![](https://images.velog.io/images/crosstar1228/post/ef2ee65d-e8f1-4317-b644-a9fa8de7c598/image.png)
## locate : 첫번째 인자의 위치를 index로 반환

```
select locate('12','ab1234');
```
- 없으면 0
- 인덱스를 1부터 계산
![](https://images.velog.io/images/crosstar1228/post/baca6640-e687-4504-a875-1b8340d98912/image.png)
## LEFT, RIGHT : 왼쪽 또는 오른쪽부터 읽기

```
select left('Crosstar\'s drawer', 8);
select right('Crosstar\'s drawer', 8);
```

![](https://images.velog.io/images/crosstar1228/post/7e30cf0b-55c1-4206-a5f0-6057b1338d58/image.png)
![](https://images.velog.io/images/crosstar1228/post/8286e1ea-18ed-4a4f-8812-65655da94e07/image.png)

## LOWER(UPPER)
```
select lower('CROSSSTAR');
```
![](https://images.velog.io/images/crosstar1228/post/480d5081-ba18-4a37-85d3-4e02290ea9d8/image.png)
## Replace(교체)

```
select replace('creepy cream', 'creepy', 'crispy')
```

![](https://images.velog.io/images/crosstar1228/post/9d384656-a969-4ee1-9e69-f17926ee408d/image.png)

## TRIM(공백 or 해당 문자 제거)
```
select TRIM('       crosstar        '),
trim(leading '#' from '###crosstar###'),
trim(trailing '#' from '###crosstar###');
```
- default 는 양쪽 공백제거
- LTRIM, RTRIM은 각 왼쪽, 오른쪽 공백 제거
- trim(both ~) : 양쪽 다 제거
- trim(leading/trailing ~) : 앞쪽 또는 뒤쪽
![](https://images.velog.io/images/crosstar1228/post/64183115-5caa-4987-ae30-1a59ec94d31e/image.png)

## FORMAT
```
#금액 표기법으로 변경& 소수점 둘째자리까지 반올림
select format(100000000.123, 2); 
```
![](https://images.velog.io/images/crosstar1228/post/d84b321b-ce84-440e-a85f-6ea206e2f48c/image.png)

##  버림, 올림, 반올림
```
select floor(5.5), ceil(5.5), round(5.5);
```

![](https://images.velog.io/images/crosstar1228/post/4697385b-9ee2-4bb7-a342-677174981049/image.png)

## 기타 수식.(제곱, 제곱근, 자연로그, 삼각함수, 절댓값, 랜덤값 생성)
```
select sqrt(9), pow(2,2), exp(2), log(exp(1)), sin(pi()/2), cos(pi()), tan(pi()/4), abs(-10), round(rand()*100, 0);
```
![](https://images.velog.io/images/crosstar1228/post/265110e6-0680-417b-a8b1-f09cbd2299b5/image.png)



# 날짜 및 시간 실습

> 오늘 11월 19일 00시를 지나고 있네요. 날짜 실습을 진행해 봅시다.

## now, curdate, curtime
- 각각 현재 시간과 날짜, 날짜, 시간 반환
```
select now(), curdate(), curtime();
```

![](https://images.velog.io/images/crosstar1228/post/59bbf93a-d066-401f-abf6-558e3357fd63/image.png)
## date에서 second까지
```
select
now(),
date(now()),
month(now()),
day(now()),
hour(now()),
minute(now()),
second(now());
```

![](https://images.velog.io/images/crosstar1228/post/be8c6270-0876-4465-89bd-9720bb1058a1/image.png)

## monthname, dayname
- 달과 날짜의 이름을 출력
```
select
now(),
monthname(now()),
dayname(now());
```

![](https://images.velog.io/images/crosstar1228/post/519c7d31-8dcc-4356-86de-773f118c1c00/image.png)

## dayofweek, dayofmonth, dayofyear
- 주/달/년에서 몇번째 날?
```
select
now(),
dayofweek(now()),
dayofmonth(now()),
dayofyear(now());
```
![](https://images.velog.io/images/crosstar1228/post/94d13a2f-0f32-495a-9694-55faa32ffcce/image.png)

## date_format
- 포맷에 맞게 출력!

```
select
date_format(now(), '%Y-%M-%D');
```
![](https://images.velog.io/images/crosstar1228/post/d013bde5-505d-449e-86bc-2e9bce748be3/image.png)


