# ApplicationContext与BeanFactory

`BeanFactory` 接口是Spring对依赖注入容器的核心，如果应用程序需要DI支持，可通过`BeanFactory`接口与Spring DI容器交互。

最常用的办法就是使用实现了`BeanFactory`接口的`ApplicationContext`配置需要注入的bean，然后在代码中通过@Autowired声明后来使用。

`ApplicationContext`是`BeanFactory`接口的扩展，除了DI，还提供了其他服务，例如事务和AOP等



