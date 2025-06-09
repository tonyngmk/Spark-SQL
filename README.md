# 0. Spark SQL
Although SQL is frowned upon by many high-browed programmers, I believe its  **simple yet powerful** is often the quickest way to learn, develop, test and maintain, while understanding the concepts from developer to developer with minimal barriers, exists not only as a great equaliser, but also a simple yet powerful tool that every corporation in the world requires for layering even complex data-models.

This repo's purpose is to dump data-manipulation techniques of Spark-SQL while serving as a notebook for past data-modelling tips.

## 1. Fundamental Operations

### 1.1 Joins

#### 1.1.1 Preventing duplicates

**Duplicates** can be frustrating and time-costly to debug but can largely be avoided through good practices while developing.

Given an `Orders` table, where `order_id` is the PK :

| order_id | from_user_id | to_user_id | gift_id | amount |
|----------|--------------|------------|---------|--------|
| 1        | 1            | 2          | 1       | 100    |
| 2        | 1            | 3          | 1       | 50     |
| 3        | 2            | 3          | 2       | 200    ||

- `GROUP BY `order_id` HAVING COUNT(*) > 1` should not have any rows.

Before joining, in case of upstream data inconsistencies, it's good practice to de-duplicate to ensure 1:1 in joins (if this operation is not computationally expensive) with:

1. `GROUP BY`
2. `DISTINCT`
3. `ROW_NUMBER`/`RANK`/`DENSE_RANK`

#### 1.1.2 Intentional duplicates

Although uncommon in most scenarios, there are cases where we would want dataset to have duplicates from join  by condition.

Say a single `video` can be considered in multiple `competition`, as long as it has been published between certain date range (and has the highest like count). 

