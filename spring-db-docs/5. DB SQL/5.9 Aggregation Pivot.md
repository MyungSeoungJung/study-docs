물론! 제품별로 그룹핑하고 년도별 합산금액을 쿼리 결과 컬럼으로 추가하는 SQL 쿼리를 아래의 예시 데이터를 기반으로 작성해보겠습니다.

`orders` 테이블:

| order_id | product_name | order_date | order_amount |
| -------- | ------------ | ---------- | ------------ |
| 1        | Product A    | 2022-12-31 | 100          |
| 2        | Product B    | 2022-12-31 | 50           |
| 3        | Product A    | 2023-01-01 | 75           |
| 4        | Product B    | 2023-01-01 | 60           |
| 5        | Product C    | 2023-01-01 | 120          |

이제 각 제품별로 그룹핑하고, 년도별로 주문 금액의 합을 계산하는 SQL 쿼리를 작성해보겠습니다.

```sql
SELECT
  product_name,
  SUM(CASE WHEN YEAR(order_date) = 2022 THEN order_amount ELSE 0 END) AS total_amount_2022,
  SUM(CASE WHEN YEAR(order_date) = 2023 THEN order_amount ELSE 0 END) AS total_amount_2023
FROM
  orders
GROUP BY
  product_name;
```

위 쿼리는 `product_name` 컬럼을 기준으로 제품별로 그룹핑하고, `CASE WHEN` 문을 사용하여 년도가 2022인 경우와 2023인 경우를 구분하여 주문 금액을 합산합니다. 이렇게 계산한 년도별 합산금액을 `total_amount_2022`와 `total_amount_2023`이라는 쿼리 결과 컬럼으로 추가하여 결과를 보여줍니다.

결과:

| product_name | total_amount_2022 | total_amount_2023 |
| ------------ | ----------------- | ----------------- |
| Product A    | 100               | 75                |
| Product B    | 50                | 60                |
| Product C    | 0                 | 120               |

이 예시에서는 `CASE WHEN` 문을 사용하여 년도가 2022와 2023인 경우를 구분하여 제품별로 주문 금액을 합산하였습니다. `SUM()` 함수와 조건절인 `CASE WHEN` 문을 함께 사용하여 데이터를 조건에 따라 다르게 처리하고, `GROUP BY` 구문을 사용하여 제품별로 그룹핑하고, `YEAR()` 함수를 사용하여 `order_date`에서 년도를 추출하였습니다.
