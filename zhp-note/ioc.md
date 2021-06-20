# IOC

## @Bean的实现
- `SpringApplication.refresh`最终会调用到 `org.springframework.context.support.AbstractApplicationContext.refresh`
```$java
//AbstractApplicationContext.refresh
				// Invoke factory processors registered as beans in the context.
				invokeBeanFactoryPostProcessors(beanFactory);
```
- `invokeBeanFactoryPostProcessors`最终会对入口的`SpringBootApplication`进行scan来找到所有的config类，并找到其中的bean,并初始化。

```
//example stack
scanCandidateComponents:437, ClassPathScanningCandidateComponentProvider (org.springframework.context.annotation)
findCandidateComponents:315, ClassPathScanningCandidateComponentProvider (org.springframework.context.annotation)
doScan:276, ClassPathBeanDefinitionScanner (org.springframework.context.annotation)
parse:132, ComponentScanAnnotationParser (org.springframework.context.annotation)
doProcessConfigurationClass:296, ConfigurationClassParser (org.springframework.context.annotation)
processConfigurationClass:250, ConfigurationClassParser (org.springframework.context.annotation)
parse:207, ConfigurationClassParser (org.springframework.context.annotation)
parse:175, ConfigurationClassParser (org.springframework.context.annotation)
processConfigBeanDefinitions:331, ConfigurationClassPostProcessor (org.springframework.context.annotation)
postProcessBeanDefinitionRegistry:247, ConfigurationClassPostProcessor (org.springframework.context.annotation)
invokeBeanDefinitionRegistryPostProcessors:311, PostProcessorRegistrationDelegate (org.springframework.context.support)
invokeBeanFactoryPostProcessors:112, PostProcessorRegistrationDelegate (org.springframework.context.support)
invokeBeanFactoryPostProcessors:746, AbstractApplicationContext (org.springframework.context.support)
refresh:564, AbstractApplicationContext (org.springframework.context.support)
refresh:145, ServletWebServerApplicationContext (org.springframework.boot.web.servlet.context)
refresh:758, SpringApplication (org.springframework.boot)
refreshContext:438, SpringApplication (org.springframework.boot)
run:337, SpringApplication (org.springframework.boot)
run:1336, SpringApplication (org.springframework.boot)
run:1325, SpringApplication (org.springframework.boot)
main:20, DemoApplication (com.example.demo)
```
