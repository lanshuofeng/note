### 1 指定配置文件启动`-Dspring.profiles.active=dev`
```shell
java -jar -Dspring.profiles.active=dev msg_app_server.jar
```

### 2 `@Profile`注解
>spring 3.2以前作用在类上
>spring 3.2以后作用在方法上

作用：   `@Profile("dev")`指定了配置生效的环境， 当`-Dspring.profiles.active=dev`时该配置生效。   [参考文档](https://www.cnblogs.com/zszxz/p/12700309.html)

### 3 `ApplicationRunner`接口
`ApplicationRunner`是一个接口,当需要在系统启动的时候加载一些自定义的配置的时候可以实现`ApplicationRunner`的`run`方法， 系统启动时会执行

### 4 `@Order` 注解
`@Order(1)`指定了 `Bean`加载的顺序， 数字越小优先级越高，可以为负数

### 5 `@ConfigurationProperties`注解
`@ConfigurationProperties`用来将配置文件的配置信息映射到`bean`,  `prefix`参数指定了读取哪个参数下的配置

yaml配置如下：
```yaml
app:
	hosts:
		origin: 123.com,456.com
```
则读取配置的代码
```java
@Configurartion
@ConfigurationProperties(prefix='app')
public MyProperty {
	private Hosts hosts;
	
	public void setHosts(Hosts hosts){this.hosts=hosts;}
	public Hosts getHosts(){return this.hosts;}
	
	public static class Hosts {
		private List<String> origin;
		
		public void setOrigin(List<String> origin){this.origin=origin;}
		
		public List<String> getOrigin(){return this.origin;}
	}
}
```
[参考文档](https://www.cnblogs.com/tian874540961/p/12146467.html)