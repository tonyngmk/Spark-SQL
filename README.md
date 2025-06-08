# 0. Spark SQL
Although SQL is frowned upon by many high-browed programmers, I believe there are many benefits:

- **💪 Simple yet powerful**: Writing in SQL is often the quickest way to learn, develop, test and maintain, while understanding the concepts from developer to developer with minimal barriers, exists not only as a great equaliser, but also a simple yet powerful tool that every corporation in the world requires for layering even complex data-models.

This repository's purpose is to dump my understand of  core concepts and ideas of data-manipulation and data-modelling, which are both key for any data developer.

## 1. Fundamental Operations

### 1.1 Joins

#### 1.1.1 Preventing duplicates

**Duplicates** can be frustrating and time-costly to debug, but can largely be avoided from good practices and some heuristics to debug.

Given an `Orders` table, where `order_id` is the PK :

| order_id | from_user_id | to_user_id | gift_id | amount |
|----------|--------------|------------|---------|--------|
| 1        | 1            | 2          | 1       | 100    |
| 2        | 1            | 3          | 1       | 50     |
| 3        | 2            | 3          | 2       | 200    ||

- `GROUP BY `order_id` HAVING COUNT(*) > 1` should not have any rows.

Say for some reason I wanted to join the field operating system (`os`) to analyse data to split by this field which does not exist and duplicated `order_id` field, this will cause an explosion and overexagerated `amount` value when we do any analysis.  

| order_id | from_user_id | from_user_os | to_user_id | gift_id | amount |
|----------|--------------|--------------|------------|---------|--------|
| 1        | 1            | android      | 2          | 1       | 100    |
| 2        | 1            | ios          | 3          | 1       | 50     |
| 1        | 1            | android      | 2          | 1       | 100    |
| 2        | 1            | ios          | 3          | 1       | 50     |
| 3        | 2            | android      | 3          | 2       | 200    |



