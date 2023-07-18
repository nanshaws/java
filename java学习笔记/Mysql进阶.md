# Mysql进阶学习

## 1.mysql的while循环

```sql
USE itheima;
DROP PROCEDURE IF EXISTS addert;
create procedure addertr()
begin
	declare a int DEFAULT 3;
    while a!=1 do
     select * from dept where  deptid = a;
     set a=a-1;
    END WHILE;
end ;
call addertr();
```

MySQL是不支持for循环语句的，MySQL支持while循环、repeat循环、loop循环

## 2.mysql的repeat循环

```sql
 repeat
            insert into test values (i);    #往test表添加数据
            set i = i + 1;                  #循环一次,i加一
 until i > 10 end repeat;                   #结束循环的条件: 当i大于10时跳出repeat循环
```

```sql
create procedure addertr1()
begin
	declare a int DEFAULT 3;
    repeat
     select * from dept where  deptid = a;
     set a=a-1;
    until a=0 end repeat;
end ;
call addertr1();
```

![image-20230309232923933](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230309232923933.png)

查询的三条数据

## 3.mysql的loop循环

```sql
lp : loop                           #lp为循环体名,可随意 loop为关键字
                insert into test values (i);    #往test表添加数据
                set i = i + 1;                  #循环一次,i加一
            if i > 10 then                  #结束循环的条件: 当i大于10时跳出loop循环
                leave lp;
            end if; 
end loop;
```

```sql
delimiter $$
create procedure addertr2()
begin
	declare a int DEFAULT 3;
   lp:loop
     select * from dept where  deptid = a;
     set a=a-1;
    if a=0 then
       leave lp;
    end if;
   end loop;
end $$
delimiter ;
call addertr2();
```

![image-20230309233947932](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230309233947932.png)







