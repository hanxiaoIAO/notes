[toc]

## 导入导出

该命令在“开始菜单>>运行>>CMD”中执行（windows）

一、数据导出（exp.exe）

```powershell
# 将数据库orcl完全导出，用户名system，密码accp，导出到d:\daochu.dmp文件中
exp system/accp@orcl file=d:\daochu.dmp full=y

# 将数据库orcl中scott用户的对象导出
exp scott/accp@orcl file=d:\daochu.dmp  owner=(scott)
	
# 将数据库orcl中的scott用户的表emp、dept导出
exp scott/accp@orcl file= d:\daochu.dmp tables=(emp,dept)

# 将数据库orcl中的表空间testSpace导出
exp system/accp@orcl file=d:\daochu.dmp tablespaces=(testSpace)
```

二、数据导入（imp.exe）

```powershell
# 将d:\daochu.dmp 中的数据导入 orcl数据库中。
imp system/accp@orcl file=d:\daochu.dmp full=y

# 如果导入时，数据表已经存在，将报错，对该表不会进行导入；加上ignore=y即可，表示忽略现有表，在现有表上追加记录。
imp scott/accp@orcl file=d:\daochu.dmp  full=y  ignore=y

# 将d:\daochu.dmp中的表emp导入
imp scott/accp@orcl file=d:\daochu.dmp tables=(emp)
```

## linux下连接数据库

```shell
# 将用户切换到Oracle
su - oracle
sqlplus / as sysdba
conn username/password
```

## 其他杂七杂八的先临时扔这

 步骤一：  删除user

drop user ×× cascade(有删除权限)
select 'drop table '||table_name||';' from cat where table_type='TABLE'（没有删除权限）
说明： 删除了user，只是删除了该user下的schema objects，是不会删除相应的tablespace的。


步骤二： 删除tablespace

DROP TABLESPACE tablespace_name INCLUDING CONTENTS AND DATAFILES;

创建表空间语句：

create tablespace user_data    datafile 'D:\ a.dbf' size 50m   autoextend on  next 50m maxsize 20480m   extent management local;

创建表空间内的用户：

create user username identified by password   default tablespace user_data;

给用户授予权限  ：

grant connect,resource,dba to username;

SQL code
--删除空的表空间，但是不包含物理文件
drop tablespace tablespace_name;
--删除非空表空间，但是不包含物理文件
drop tablespace tablespace_name including contents;
--删除空表空间，包含物理文件
drop tablespace tablespace_name including datafiles;
--删除非空表空间，包含物理文件
drop tablespace tablespace_name including contents and datafiles;
--如果其他表空间中的表有外键等约束关联到了本表空间中的表的字段，就要加上CASCADE CONSTRAINTS
drop tablespace tablespace_name including contents and datafiles CASCADE CONSTRAINTS;


      1、设置表空间自动扩展与否

alter database datafile 文件路径 autoextend off；取消自动扩展

alter database datafile 文件路径 autoextend on；设置自动扩展

2、设置默认表空间

alter database default tablespace XXX;   整个数据库的，新建用户时不指定表空间则会默认这个。

alter user tanyixiu default tablespace smilespace; 只更改这个用户的.

3、查看用户默认表空间

select username,default_tablespace from dba_users where username='XXX'；

4、表空间更名

alter tablespace XXX rename to YYY;

5、更改表空间文件路径

    在線移
    
    1).alter tablespace tablespace_name offline; 
    
    2).os下copy d:\oradata\ datafilename to G:\oradata\datafilename 
    
    3).alter tablespace tablespace_name rename datafile 'd:\oradata\ datafilename' to 'G:\oradata\datafilename';
    
    4).alter tablespace tablespace_name online;
    
    不在線移
    
    1).startup mount
    
    2).os下copy d:\oradata\ datafilename to G:\oradata\datafilename 
    
    3).alter tablespace tablespace_name rename datafile 'd:\oradata\ datafilename' to 'G:\oradata\datafilename';
    
    4).alter database open



