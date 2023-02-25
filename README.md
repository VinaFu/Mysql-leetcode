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

3. 1699

      Question:
      建表命名，计数 + 不重复计数（null）；分别计数；排序
      
      Solution:
      
            SELECT date_id, make_name, COUNT(DISTINCT lead_id) AS unique_leads, COUNT(DISTINCT partner_id) AS unique_partners
            FROM DailySales
            GROUP BY date_id, make_name
            ORDER BY date_id, make_name;
                        // 计数：count；非重复： distinct; 用了distinct不能用count(*)
                        // 顺序：group > order

4. 


