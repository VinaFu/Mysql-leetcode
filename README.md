# Mysql-leetcode
Easy to Medium(1751,1741,1693,1393)

1. 1751

      Question: 
      找出low_fats 和 recyclable 都等于"Y"的产品名字

      Solution:
      
            SELECT product_id
            From Products
            WHERE (low_fats = "Y" AND recyclable ="Y");
                      // where注意打括号，引用字符要用引号
                      // 语法结束要用分号
           
2. 1741

      Question:
      同样ID同一天的外出时间-内在时间；
      表格换名字
      
      Solution:
      
            SELECT event_day AS day, emp_id , SUM(out_time - in_time) AS total_time
            From Employees
            GROUP BY day, emp_id;
                        // 换名字用AS，可以有运算：SUM
                        // 同样参数用GROUP BY放在一起。
                        // 见12-13章内容

3. 1693

      Question:
      建表命名，计数 + 不重复计数（null）；分别计数；排序
      
      Solution:
      
            SELECT date_id, make_name, COUNT(DISTINCT lead_id) AS unique_leads, COUNT(DISTINCT partner_id) AS unique_partners
            FROM DailySales
            GROUP BY date_id, make_name
            ORDER BY date_id, make_name;
                        // 计数：count；非重复： distinct; 用了distinct不能用count(*)
                        // 顺序：group > order

4. 1393

      Question:
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

5. 1795

      Qestion:
      rearrange the table, use of Union and PIVOT
      将不同的列名放入同一列()
      
      Solution:
      
      5.1 Union:
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

      5.2 PIVOT:
            SELECT product_id,store,price
            FROM Products
            UNPIVOT
            (
                  price
                  FOR store in (store1,store2,store3)
            ) AS T


