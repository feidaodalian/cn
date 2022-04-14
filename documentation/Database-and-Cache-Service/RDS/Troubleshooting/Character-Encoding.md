# 云数据库 MySQL 字符集编码问题
字符集是一个在使用数据库过程中经常碰到的问题，然后很多同学对这块的使用其实不是很了解，所以会经常出现在使用过程中乱码的情况，今天我们来具体讲讲字符集相关问题，从容应对乱码问题。

## 查看字符集
首先我们得先登录云数据库 RDS 实例看看当前字符集的设置是怎么样的，当你通过远程连接到数据库实例之后，通过命令选择你需要使用的库，命令如下：

```SQL
use <库名>
```
执行完上面的命令，你就进入到了一个库中，然后执行如下命令：

```SQL
show variables like '%character%'
```
可以看到字符集的具体情况如下

|variable_name|value|
|---|---|
|character\_set_client|	utf8|
|character\_set_connection|	utf8|
|character\_set_database	|utf8|
|character\_set_filesystem|	binary|
|character\_set_results	|utf8|
|character\_set_server|	utf8|
|character\_set_system	|utf8|

## 字符集剖析
### character\_set_client
此参数是客户端可以设置的，具体设置方式见下文详解。

### character\_set_connection
此参数是客户端可以设置的，具体设置方式见下文详解。

### character\_set_database
此参数值与你创建库的时候指定的字符集有关，关于创建库的时候如何指定字符集，可以参考[创建库](../Operation-Guide/Database-Management/Create-Database.md)

### character\_set_filesystem
此参数可以不用关心

### character\_set_results
此参数是客户端可以设置的，具体设置方式见下文详解。

### character\_set_server
此参数是服务端的设置，此参数值可以通过参数组进行修改，可以参考 [修改参数](../Operation-Guide/Parameter-Group/Modify-Parameter.md)；注意：此参数修改完后，记得重启实例才能确保 `character_set_database` 默认值与 `character_set_server` 保持同步。

### character\_set_system
此参数可以不用关心

## 客户端设置字符集
上面提到了`character_set_client`、`character_set_connection `、`character_set_results` 这三个参数值是会话级别的，可以通过客户端进行设置的，当你连接上云数据库 RDS 实例后，执行以下 SQL 指令：

```SQL
set names <字符集编码>;
```
执行成功后，这三个参数值会被设置成相应的字符集编码；

注意：因为是会话级别的，所以当你重连数据库实例之后，原先的字符集设置会失效，需要重新执行下 `set names` 命令进行设置。

## 如何避免乱码
要避免在使用数据库过程中的乱码问题，需要确保`character_set_client`、`character_set_connection `、`character_set_results`、`character_set_database`这四个参数值是保持一致的，如果不一致就会有可能出现乱码。

## 最佳实践
### 如何存储 emoji 表情
如果要在云数据库 RDS 实例中存储 emoji 表情，请确保`character_set_client`、`character_set_connection `、`character_set_results`、`character_set_database`这四个参数组值都是 ***utf8mb4***。

通过客户端设置字符集的 c++ 示例代码如下, 仅供参考
```SQL
string sql = "set names utf8mb4";
mysql_query(connection, sql.c_str());
```
