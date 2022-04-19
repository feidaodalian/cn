# 审计介绍

## 特点和优势
1. 基于SQL Server原生的审计功能，审计全面、无遗漏；
2. 用户可自定义审计策略，满足不同业务场景的需求；
3. 审计结果为二进制，无法篡改，安全性好；
3. 审计功能无额外费用，用户可免费使用；
4. 审计文件保存6个月，满足的合规要求；


## 审计选项
关于实例级的每个审计项的具体说明，可以参考微软相应版本的官方文档：

- [2008R2](https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008-r2/cc280663%28v%3dsql.105%29)
- [2012](https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2012/cc280663%28v%3dsql.110%29)
- [2014](https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2012/cc280663%28v%3dsql.110%29)
- [2016](https://docs.microsoft.com/zh-cn/sql/relational-databases/security/auditing/sql-server-audit-action-groups-and-actions?view=sql-server-2016)

## 备注
- 关闭审计时，审计结果文件不会被删除，还是会保存6个月；
- 审计文件每30分钟会上传到云存储上供用户下载，因此控制台的审计结果文件大约有30分钟的延迟；
