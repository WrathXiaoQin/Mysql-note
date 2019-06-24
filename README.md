# Mysql-note
Record notes

## case聚合用法
```mysql
SELECT std_id,
CASE WHEN COUNT(*) = 1 -- 只加入了一个社团的学生
THEN MAX(club_id)
ELSE MAX(CASE WHEN main_club_flg =  ' Y '
THEN club_id
ELSE NULL END)
END AS main_club
FROM StudentClub
GROUP BY std_id;
```

## 集合特性用法
```mysql
No 条件表达式 用途
1 COUNT (DISTINCT col) = COUNT (col) col 列没有重复的值
2 COUNT(*) = COUNT(col) col 列不存在 NULL
3 COUNT(*) = MAX(col) col 列是连续的编号（起始值是 1）
4 COUNT(*) = MAX(col) - MIN(col) + 1 col 列是连续的编号（起始值是任意整数）
5 MIN(col) = MAX(col) col 列都是相同值，或者是 NULL
6 MIN(col) * MAX(col) > 0 col 列全是正数或全是负数
7 MIN(col) * MAX(col) < 0 col 列的最大值是正数，最小值是负数
8 MIN(ABS(col)) = 0 col 列最少有一个是 0
9 MIN(col - 常量 ) = - MAX(col - 常量 ) col 列的最大值和最小值与指定常量等距
```
