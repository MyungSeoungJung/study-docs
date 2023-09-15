물론! SQL의 `SUM()` 함수를 사용하여 제품별과 연도별로 그룹핑하여 주문 금액의 합계를 계산하는 쿼리를 아래의 예시 데이터를 기반으로 작성해보겠습니다.

`orders` 테이블:

| order_id | product_name | order_date | order_amount |
| -------- | ------------ | ---------- | ------------ |
| 1        | Product A    | 2022-12-31 | 100          |
| 2        | Product B    | 2022-12-31 | 50           |
| 3        | Product A    | 2023-01-01 | 75           |
| 4        | Product B    | 2023-01-01 | 60           |
| 5        | Product C    | 2023-01-01 | 120          |

이제 제품별과 연도별로 그룹핑하여 주문 금액의 합계를 계산하는 SQL 쿼리를 작성해보겠습니다.

```sql
SELECT
  product_name,
  YEAR(order_date) AS order_year,
  SUM(order_amount) AS total_amount
FROM
  orders
GROUP BY
  product_name,
  YEAR(order_date);
```

위 쿼리는 `product_name`과 `YEAR(order_date)`를 기준으로 그룹핑하고, `SUM()` 함수를 사용하여 주문 금액의 합계를 계산합니다. 이렇게 계산한 결과를 `total_amount`라는 컬럼으로 보여줍니다.

결과:

| product_name | order_year | total_amount |
| ------------ | ---------- | ------------ |
| Product A    | 2022       | 100          |
| Product A    | 2023       | 75           |
| Product B    | 2022       | 50           |
| Product B    | 2023       | 60           |
| Product C    | 2023       | 120          |

이 예시에서는 `SUM()` 함수를 사용하여 제품별과 연도별로 주문 금액을 합산하였습니다. `GROUP BY` 구문을 사용하여 `product_name`과 `YEAR(order_date)`를 기준으로 그룹핑하고, 연도를 추출하기 위해 `YEAR()` 함수를 사용하였습니다. 결과적으로 제품별, 연도별로 주문 금액의 합계를 계산하고, 해당 결과를 `total_amount` 컬럼으로 보여줍니다.
