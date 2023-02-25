# Mysql-leetcode
Easy to Medium(1751,1741,1693,1393)

1. 1751


  Question: 
  找出low_fats 和 recyclable 都等于"Y"的产品名字

  Solution:
    SELECT product_id
    From Products
    WHERE (low_fats = "Y" AND recyclable ="Y");
