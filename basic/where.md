> where문을 어떻게 활용할 수 있을지 알아봅시다.

## table 모양 확인
![](https://images.velog.io/images/crosstar1228/post/9288b936-0ef3-45d4-8f4f-f0540da5d69b/image.png)

### 1. AND(OR)

```
select CountryCode, District
from city
where countrycode='KOR' AND District='Seoul';
```
![](https://images.velog.io/images/crosstar1228/post/6436f95c-46b3-4676-af6a-9107b0e57f96/image.png)

### 2. BETWEEN(수치 값)
```
select * from city where population between 100000 and 300000;

```
![](https://images.velog.io/images/crosstar1228/post/6f0e24fe-4ba9-4ffb-a2c2-1413695871d7/image.png)

### 3. IN

```
select * from city
where name in ('Kabul', 'Seoul', 'Tokyo');
```
![](https://images.velog.io/images/crosstar1228/post/78fe3d53-5ac7-479f-83e8-edc9c236148a/image.png)

### 4. LIKE
```
# New로시작하는 모든 값들 출력
select * from city where Name LIKE 'New%';
```
![](https://images.velog.io/images/crosstar1228/post/a5748243-4113-4f8b-a2be-3a0f9a3f2ae3/image.png)