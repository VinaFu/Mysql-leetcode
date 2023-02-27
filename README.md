# Mysql-leetcode
Easy to Medium(1751,1741,1693,1393)

1. 1751      Question: 
      找出low_fats 和 recyclable 都等于"Y"的产品名字

      Solution:
      
            SELECT product_id
            From Products
            WHERE (low_fats = "Y" AND recyclable ="Y");
                      // where注意打括号，引用字符要用引号
                      // 语法结束要用分号
           
2. 1741      Question:
      同样ID同一天的外出时间-内在时间；
      表格换名字
      
      Solution:
      
            SELECT event_day AS day, emp_id , SUM(out_time - in_time) AS total_time
            From Employees
            GROUP BY day, emp_id;
                        // 换名字用AS，可以有运算：SUM
                        // 同样参数用GROUP BY放在一起。
                        // 见12-13章内容

3. 1693      Question:
      建表命名，计数 + 不重复计数（null）；分别计数；排序
      
      Solution:
      
            SELECT date_id, make_name, COUNT(DISTINCT lead_id) AS unique_leads, COUNT(DISTINCT partner_id) AS unique_partners
            FROM DailySales
            GROUP BY date_id, make_name
            ORDER BY date_id, make_name;
                        // 计数：count；非重复： distinct; 用了distinct不能用count(*)
                        // 顺序：group > order

4. 1393      Question:
      建表命名, 数学用法. CASE 运行算法 (遇到“buy”转为负数)
      
      Solution:
      
            SELECT stock_name, SUM(
                CASE 
                    WHEN operation = 'buy' THEN -price
                    ELSE price
                END
            ) AS capital_gain_loss
            FROM Stocks
            GROUP BY stock_name;
                  // meet "buy" changes it into -; then sum, so the CASE is inside the SUM
                  // can be used in any position, where/ group by/ select, etc.
                  // CASE - END; WHEN THEN, ELSE.
                  // See more syntax in: https://www.w3schools.com/sql/func_mysql_case.asp

5. 1795      Qestion:
      重新排列表格:
      将不同的列名放入同一列(); use of Union
      
      Solution:
      
            SELECT product_id, 'store1' AS store, store1 AS price 
            FROM Products 
            WHERE store1 IS NOT NULL
            UNION 
            SELECT product_id, 'store2' AS store, store2 AS price 
            FROM Products 
            WHERE store2 IS NOT NULL
            UNION 
            SELECT product_id, 'store3' AS store, store3 AS price 
            FROM Products 
            WHERE store3 IS NOT NULL
            ORDER BY product_id, store;
                        // "store1", 将一项放入新列
                        // store1 AS price, 将值放入另一列
                        // UNION 运算符用于组合两个或多个 SELECT 语句的结果集。最后一个不要UNION
                        // 因为终表剔除了null值，所以 WHERE store1/2/3 IS NOT NULL

6. 176 Question: 选择第二大值

      Solution:
      
      6.1 MAX
      
            SELECT MAX(salary) AS SecondHighestSalary
            FROM Employee
            WHERE salary < (SELECT MAX(salary) FROM Employee);
                        // 选择最大的一个 - MAX()
                        // 然后选择比它小的那个，那是第二大的
                        // 仅当我们选择第二个/第三个时才适用; 不适用于 n-th

      6.2 DISTINCT && LIMIT
      
            SELECT
            (SELECT DISTINCT salary 
            FROM Employee 
            ORDER BY salary DESC
            LIMIT 1, 1)
            AS SecondHighestSalary;
                        // 主要 AS 语法正确。在中间使用 从句
                        // DISTINCT - 每一个计数; 100, 100 = 2 items
                        // ORDER BY ... DESC LIMIT 1,1 = NO.2 , 1 
                                             LIMIT 0,1 = NO.1, 1
                        // LIMIT 3 = 选择 3 项

7. 177 n-th highest

      Solution:
      
      CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
      BEGIN
          SET N = N-1;        // Fix the Index
          RETURN (
            # Write your MySQL query statement below.
              SELECT DISTINCT salary
              FROM Employee
              ORDER BY salary DESC
              LIMIT N, 1
                              // just like the one above: DISTINCT/ DESC/ LIMIT
                              // LIMIT N, 1 = LIMIT 1 OFFSET N (offset = starts with; limit = how many)
                              
        );
      END



