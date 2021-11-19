> group by 문을 어떻게 활용할 수 있을지 알아봅시다.

## table 모양 확인
![](https://images.velog.io/images/crosstar1228/post/9288b936-0ef3-45d4-8f4f-f0540da5d69b/image.png)


** having : where문과 유사하나 group by 와 함꼐 이용
** 
## having, order by, limit
국가코드에 따른 인구의 최댓값, 그리고 해당 도시 이름을출력하되, 
 - 칼럼명을 '인구수'로 바꾸고
 - 십만명 이상인 곳만 추출하고
 - 오름차순으로 정리하고
 - 15개 행만 출력
```
select Name, CountryCode, MAX(Population) AS '인구수' from city group by Countrycode having MAX(Population) > 100000 order by MAX(Population) ASC limit 15;
```
![](https://images.velog.io/images/crosstar1228/post/a60a7b07-4533-4309-afe3-5d9c0b4cc171/image.png)



## with rollup(총합계 또는 중간집계 필요 시)
1. 나라코드에 따른 인구 수 합계를 출력하고, 총합계를 맨 아래에 출력
```
select CountryCode, sum(population) from city group by Countrycode with rollup ;

```

![](https://images.velog.io/images/crosstar1228/post/effdf660-8d95-4d7b-af0f-54aadd764980/image.png)

2. **도시**에 따른 도시의 인구 수를 출력하고 나라코드별 인구 수 **중간합계를 매 나라코드별** 출력
```
select CountryCode, Name, sum(Population) from city group by countrycode, Name with rollup; 

```
![](https://images.velog.io/images/crosstar1228/post/45f615ca-da07-4895-bf2c-e93d93c4ad06/image.png)


### Groupby와 함께 사용되는 집계 함수

- AVG() : 평균
- MIN() : 최소값
- MAX() : 최대값
- COUNT() : 행의 개수
- COUNT(DISTINCT) : 중복 제외한 행의 개수
- STDEV() : 표준 편차
- VARIANCE() : 분산