1. 导出数据库名为dbname的所有表结构
```shell
 mysqldump -uroot -pdbpasswd -d dbname >db.sql;
```
2. 导出数据库名为dbname的test表的结构
```shell
mysqldump -uroot -pdbpasswd -d dbname test>db.sql;
```

3. 导出数据库名为dbname的所有表结构和数据 不加 -d
```shell
mysqldump -uroot -pdbpasswd  dbname >db.sql;
```

4. 导出数据库名为dbname的某张表（test）的结构和数据
```shell
mysqldump -uroot -pdbpasswd dbname test>db.sql;
```
5. 导出数据到压缩文件
```shell
mysqldump -uroot -p123456 库名字 | gzip > online.sql.gz
```
6.讲导出的sql文件下载到本地：
```shell
scp root@ip:/目录/文件 .
```
