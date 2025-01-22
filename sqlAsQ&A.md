# SQL의 `AS` 키워드 사용 범위

---

### Q: `AS`는 `SELECT`에서만 사용 가능한가요?
A: 아닙니다! `AS` 키워드는 `SELECT`문에서만 사용되는 것이 아니라, SQL의 다양한 문장에서 활용될 수 있습니다. 주요 사용 사례는 다음과 같습니다.

---

### Q: `SELECT` 문에서 `AS`는 어떻게 사용되나요?
A: 테이블 열(column)이나 계산 결과에 별칭을 부여합니다.

```sql
SELECT column_name AS alias_name
FROM table_name;
```

예:
```sql
SELECT first_name AS 이름, last_name AS 성
FROM employees;
```

---

### Q: 테이블에 별칭을 부여하려면 어떻게 하나요?
A: 테이블 이름이 길거나 가독성을 높이기 위해 `FROM` 또는 `JOIN` 절에서 테이블에 별칭을 부여합니다.

```sql
SELECT e.first_name, d.department_name
FROM employees AS e
JOIN departments AS d
ON e.department_id = d.department_id;
```

여기서 `employees`는 `e`로, `departments`는 `d`로 별칭을 부여했습니다.

---

### Q: 서브쿼리에서 `AS`는 어떻게 사용되나요?
A: 서브쿼리의 결과에 별칭을 부여하여 메인 쿼리에서 사용합니다.

```sql
SELECT subquery_result.alias_name
FROM (
    SELECT department_id, COUNT(*) AS employee_count
    FROM employees
    GROUP BY department_id
) AS subquery_result;
```

---

### Q: `WITH` 절(CTE)에서 `AS`는 어떻게 사용되나요?
A: Common Table Expression(CTE)에서도 별칭을 사용할 수 있습니다.

```sql
WITH EmployeeCount AS (
    SELECT department_id, COUNT(*) AS total_employees
    FROM employees
    GROUP BY department_id
)
SELECT d.department_name, ec.total_employees
FROM departments d
JOIN EmployeeCount ec
ON d.department_id = ec.department_id;
```

---

### Q: `INSERT`, `UPDATE`, `DELETE` 문에서도 `AS`를 사용할 수 있나요?
A: `AS`는 일반적으로 `INSERT`, `UPDATE`, `DELETE`와는 잘 사용되지 않지만, **`MERGE`문** 또는 복잡한 쿼리 구조에서 사용될 수 있습니다.

---

### Q: 요약하면 `AS`는 어디에 주로 사용되나요?
A: 
- **`SELECT`**: 열과 테이블 모두에서 매우 자주 사용됨.
- **`FROM`/`JOIN`**: 테이블에 별칭을 부여할 때 사용.
- **`WITH`/서브쿼리**: 서브쿼리나 CTE에서 결과에 별칭을 부여.
- **`INSERT`, `UPDATE`, `DELETE`**: 일반적으로 사용하지 않음.

`AS`는 **가독성을 높이고 쿼리를 간결하게 만드는 도구**로 다양한 곳에서 활용할 수 있습니다! 😊
