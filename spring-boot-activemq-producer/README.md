# spring-boot-cache-redis, 依赖spring-boot-parent
* [spring-boot](http://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
* [ActiveMQ](http://activemq.apache.org/)

```xml
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-jms</artifactId>
</dependency>
<dependency>
	<groupId>org.apache.activemq</groupId>
	<artifactId>activemq-client</artifactId>
</dependency>
<dependency>
	<groupId>org.apache.activemq</groupId>
	<artifactId>activemq-spring</artifactId>
</dependency>
```

```java
@Configuration
@Description(value = "ActiveMQ Configuration")
public class ActiveMQConfig {
	public static final String QUEUE_HELLO = "queue.hello";
	
	@Bean(name="helloQueue")
	public Queue helloQueue() {
		return new ActiveMQQueue(QUEUE_HELLO);
	}
	
	@Bean(name="jmsTemplate")
	public JmsTemplate jmsTemplate(ActiveMQConnectionFactory connectionFactory ) {
		JmsTemplate template = new JmsTemplate(connectionFactory);
		template.setDefaultDestination(helloQueue());
		template.setMessageConverter(new SimpleMessageConverter());
		return template;
	}
}
```
###application.properties
```properties
# ACTIVEMQ (ActiveMQProperties)
spring.activemq.broker-url=tcp://10.0.2.95:61616
spring.activemq.in-memory=true
spring.activemq.pooled=false
```
