### database
- table, index, 저장된 procedure 등 몇몇 구성물의 모음

### table
- column과 row로 이루어진 이차원 구조
- database 안에 포함되는 개념


## 실습
```
show databases
```
![](https://images.velog.io/images/crosstar1228/post/139f8c38-1a0f-4308-805c-b23c79e73239/image.png)

```
## world 라는 이름의 database를 사용한다
use world;
## world database 안의 table을 확인한다
show tables;
```
![](https://images.velog.io/images/crosstar1228/post/a55e727c-edbf-4d5a-ad6d-f6aec20b318c/image.png)

이제 table의 구조이므로 select와 from 을 이용하여 데이터를 본격적으로 추출 가능하다.

```
select * from city;
```
![](https://images.velog.io/images/crosstar1228/post/4c047fdf-ebd9-41c3-8a2e-3ab8daf60ec1/image.png)