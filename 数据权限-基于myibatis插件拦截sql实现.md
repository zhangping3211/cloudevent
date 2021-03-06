mybatis：自定义实现拦截器插件Interceptor

首先熟悉一下Mybatis的执行过程：
![image](https://github.com/zhangping3211/cloudevent/blob/main/img/myibatis_process.png)

先说明Mybatis中可以被拦截的类型具体有以下四种：
1.Executor：拦截执行器的方法。
2.ParameterHandler：拦截参数的处理。
3.ResultHandler：拦截结果集的处理。
4.StatementHandler：拦截Sql语法构建的处理。

Intercepts注解需要一个Signature(拦截点)参数数组。通过Signature来指定拦截哪个对象里面的哪个方法。@Intercepts注解定义如下:

@Intercepts({//注意看这个大花括号，也就这说这里可以定义多个@Signature对多个地方拦截，都用这个拦截器
@Signature(
type = ResultSetHandler.class,
method = "handleResultSets",
args = {Statement.class}),
@Signature(type = Executor.class,
method = "query",
args = {MappedStatement.class, Object.class, RowBounds.class, ResultHandler.class})
})

说明：
@Intercepts：标识该类是一个拦截器；
@Signature：指明自定义拦截器需要拦截哪一个类型，哪一个方法；
- type：上述四种类型中的一种；
- method：对应接口中的哪类方法（因为可能存在重载方法）；
- args：对应哪一个方法的入参；
  method中对应四种的类型的方法：

![img](https://github.com/zhangping3211/cloudevent/raw/main/img/method4.png)

示例：

@Intercepts({@Signature(type = StatementHandler.class, method = "prepare", args = {Connection.class, Integer.class})})
public class PrepareInterceptor implements Interceptor {

    public Object intercept(Invocation invocation) throws Throwable {
        StatementHandler statementHandler = (StatementHandler) PluginUtils.realTarget(invocation.getTarget());
        MetaObject metaObject = SystemMetaObject.forObject(statementHandler);
        MappedStatement mappedStatement = (MappedStatement) metaObject.getValue("delegate.mappedStatement");
        // 从配置信息中获取配置，没有配置则不进行处理
        String authSql;
        try {
            authSql = DataLimitConfig.getAuthSql(mappedStatement.getId());
        } catch (Exception e) {
            throw new RuntimeException("Failed to execute generateSql " + e.getMessage());
        }
        if (authSql == null || "".equals(authSql)) {
            return invocation.proceed();
        }

        // 给目标sql加上数据权限
        BoundSql boundSql = (BoundSql) metaObject.getValue("delegate.boundSql");
        String sql = boundSql.getSql();
        // 对sql中的limit和order by做处理
        String suffixSql = "";
        int lastOrderByIndex = sql.lastIndexOf("order by");
        if (lastOrderByIndex > 0) {
            suffixSql = sql.substring(lastOrderByIndex);
            sql = sql.substring(0, lastOrderByIndex);
            // 如果suffixSql中包含select，就无法确定加上数据权限sql之后是正确的，这里退出sql处理
            // todo 判断suffixSql是否合法需要优化
            if (suffixSql.indexOf("select") > 0) {
                throw new RuntimeException("add controller sql error");
            }
        }

        // 对sql中的limit做处理
        int lastLimitIndex = sql.lastIndexOf("limit");
        if (lastLimitIndex > 0 && "".equals(suffixSql)) {
            suffixSql = sql.substring(lastLimitIndex);
            sql = sql.substring(0, lastLimitIndex);
            // 如果suffixSql中包含? ，空格 之外的其他字符，就无法确定加上数据权限sql之后是正确的，这里退出sql处理
            char[] arr = suffixSql.toCharArray();
            for (int i = 5; i < arr.length; i++) {
                if (arr[i] != 44 && arr[i] != 32 && arr[i] != 63) {
                    throw new RuntimeException("add control sql error");
                }
            }
        }
        String convertSql = sql + authSql + suffixSql;
        metaObject.setValue("delegate.boundSql.sql", convertSql);
        return invocation.proceed();
    }

    public Object plugin(Object o) {
        if (o instanceof StatementHandler) {
            return Plugin.wrap(o, this);
        }
        return o;
    }

    public void setProperties(Properties properties) {

    }
}
















