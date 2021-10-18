# MyBatis笔记

## 一、软件的三层架构 

**三层架构**

- 界面层：和用户交互的，接收用户请求的参数，显示处理结果。(html、jsp、servlet)
- 业务逻辑层：接收界面层传递的参数，处理相关的业务，调用数据库获取数据……
- 数据访问层：访问数据库，对数据进行增、删、改、查等操作。

**三层架构对应的包**

- 界面层：controller包(servlet)
- 业务逻辑层：service包(xxxService类)
- 数据访问层：dao包(xxxxDao类)

**三层对应的处理框架**

界面层：servlet——Springmvc(框架)

业务逻辑层：Service类——Spring(框架)

数据持久层：dao类——MyBatis(框架)



