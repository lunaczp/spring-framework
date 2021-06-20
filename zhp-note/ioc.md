# IOC

## @Bean的实现
```$xslt
//找到并注册Bean
registerBeanDefinition:1025, DefaultListableBeanFactory (org.springframework.beans.factory.support)
loadBeanDefinitionsForBeanMethod:295, ConfigurationClassBeanDefinitionReader (org.springframework.context.annotation)
loadBeanDefinitionsForConfigurationClass:153, ConfigurationClassBeanDefinitionReader (org.springframework.context.annotation)
loadBeanDefinitions:129, ConfigurationClassBeanDefinitionReader (org.springframework.context.annotation)
processConfigBeanDefinitions:343, ConfigurationClassPostProcessor (org.springframework.context.annotation)
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

```$xslt
//实例化Bean
build:12, Config (com.example.demo.config)
CGLIB$build$0:-1, Config$$EnhancerBySpringCGLIB$$101a3ef7 (com.example.demo.config)
invoke:-1, Config$$EnhancerBySpringCGLIB$$101a3ef7$$FastClassBySpringCGLIB$$c27dc437 (com.example.demo.config)
invokeSuper:244, MethodProxy (org.springframework.cglib.proxy)
intercept:331, ConfigurationClassEnhancer$BeanMethodInterceptor (org.springframework.context.annotation)
build:-1, Config$$EnhancerBySpringCGLIB$$101a3ef7 (com.example.demo.config)
invoke0:-1, NativeMethodAccessorImpl (jdk.internal.reflect)
invoke:62, NativeMethodAccessorImpl (jdk.internal.reflect)
invoke:43, DelegatingMethodAccessorImpl (jdk.internal.reflect)
invoke:566, Method (java.lang.reflect)
instantiate:154, SimpleInstantiationStrategy (org.springframework.beans.factory.support)
instantiate:653, ConstructorResolver (org.springframework.beans.factory.support)
instantiateUsingFactoryMethod:486, ConstructorResolver (org.springframework.beans.factory.support)
instantiateUsingFactoryMethod:1334, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
createBeanInstance:1177, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
doCreateBean:564, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
createBean:524, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
lambda$doGetBean$0:335, AbstractBeanFactory (org.springframework.beans.factory.support)
getObject:-1, 96039159 (org.springframework.beans.factory.support.AbstractBeanFactory$$Lambda$325)
getSingleton:234, DefaultSingletonBeanRegistry (org.springframework.beans.factory.support)
doGetBean:333, AbstractBeanFactory (org.springframework.beans.factory.support)
getBean:208, AbstractBeanFactory (org.springframework.beans.factory.support)
preInstantiateSingletons:944, DefaultListableBeanFactory (org.springframework.beans.factory.support)
finishBeanFactoryInitialization:918, AbstractApplicationContext (org.springframework.context.support)
refresh:583, AbstractApplicationContext (org.springframework.context.support)
refresh:145, ServletWebServerApplicationContext (org.springframework.boot.web.servlet.context)
refresh:758, SpringApplication (org.springframework.boot)
refreshContext:438, SpringApplication (org.springframework.boot)
run:337, SpringApplication (org.springframework.boot)
run:1336, SpringApplication (org.springframework.boot)
run:1325, SpringApplication (org.springframework.boot)
main:20, DemoApplication (com.example.demo)
```

```$xslt
//核心流程
//org.springframework.context.support.AbstractApplicationContext
...
	@Override
	public void refresh() throws BeansException, IllegalStateException {
		synchronized (this.startupShutdownMonitor) {
			StartupStep contextRefresh = this.applicationStartup.start("spring.context.refresh");

			// Prepare this context for refreshing.
			prepareRefresh();

			// Tell the subclass to refresh the internal bean factory.
			ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();

			// Prepare the bean factory for use in this context.
			prepareBeanFactory(beanFactory);

			try {
				// Allows post-processing of the bean factory in context subclasses.
				postProcessBeanFactory(beanFactory);

				StartupStep beanPostProcess = this.applicationStartup.start("spring.context.beans.post-process");
				// Invoke factory processors registered as beans in the context.
				invokeBeanFactoryPostProcessors(beanFactory);//zhp 找到并注册bean

				// Register bean processors that intercept bean creation.
				registerBeanPostProcessors(beanFactory);
				beanPostProcess.end();

				// Initialize message source for this context.
				initMessageSource();

				// Initialize event multicaster for this context.
				initApplicationEventMulticaster();

				// Initialize other special beans in specific context subclasses.
				onRefresh();

				// Check for listener beans and register them.
				registerListeners();

				// Instantiate all remaining (non-lazy-init) singletons.
				finishBeanFactoryInitialization(beanFactory);//zhp 完成bean的实例化

				// Last step: publish corresponding event.
				finishRefresh();
			}
...
```
## @Component @Service @Repository的实现
```$xslt
//找到并注册
registerBeanDefinition:1025, DefaultListableBeanFactory (org.springframework.beans.factory.support)
registerBeanDefinition:164, BeanDefinitionReaderUtils (org.springframework.beans.factory.support)
registerBeanDefinition:320, ClassPathBeanDefinitionScanner (org.springframework.context.annotation)
doScan:292, ClassPathBeanDefinitionScanner (org.springframework.context.annotation)
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

```$xslt
//实例化
<init>:17, TestController (com.example.demo.controller)
newInstance0:-1, NativeConstructorAccessorImpl (jdk.internal.reflect)
newInstance:62, NativeConstructorAccessorImpl (jdk.internal.reflect)
newInstance:45, DelegatingConstructorAccessorImpl (jdk.internal.reflect)
newInstance:490, Constructor (java.lang.reflect)
instantiateClass:212, BeanUtils (org.springframework.beans)
instantiate:87, SimpleInstantiationStrategy (org.springframework.beans.factory.support)
instantiateBean:1308, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
createBeanInstance:1214, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
doCreateBean:564, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
createBean:524, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
lambda$doGetBean$0:335, AbstractBeanFactory (org.springframework.beans.factory.support)
getObject:-1, 295640874 (org.springframework.beans.factory.support.AbstractBeanFactory$$Lambda$325)
getSingleton:234, DefaultSingletonBeanRegistry (org.springframework.beans.factory.support)
doGetBean:333, AbstractBeanFactory (org.springframework.beans.factory.support)
getBean:208, AbstractBeanFactory (org.springframework.beans.factory.support)
preInstantiateSingletons:944, DefaultListableBeanFactory (org.springframework.beans.factory.support)
finishBeanFactoryInitialization:918, AbstractApplicationContext (org.springframework.context.support)
refresh:583, AbstractApplicationContext (org.springframework.context.support)
refresh:145, ServletWebServerApplicationContext (org.springframework.boot.web.servlet.context)
refresh:758, SpringApplication (org.springframework.boot)
refreshContext:438, SpringApplication (org.springframework.boot)
run:337, SpringApplication (org.springframework.boot)
run:1336, SpringApplication (org.springframework.boot)
run:1325, SpringApplication (org.springframework.boot)
main:20, DemoApplication (com.example.demo)
```

__说明__, 如上，`@Bean`,`@Component`的处理流程是一样的/一套代码。都是在`ApplicationContext`的`refresh`中发起。
- `invokeBeanFactoryPostProcessors`发起注册
- `finishBeanFactoryInitialization`发起实例化
```$xslt
//注册处理器
//org.springframework.context.annotation.ConfigurationClassPostProcessor
...
		do {
			StartupStep processConfig = this.applicationStartup.start("spring.context.config-classes.parse");
			parser.parse(candidates);//会对configuration class进行解析，并注册bean
			parser.validate();

			Set<ConfigurationClass> configClasses = new LinkedHashSet<>(parser.getConfigurationClasses());
			configClasses.removeAll(alreadyParsed);

			// Read the model and create bean definitions based on its content
			if (this.reader == null) {
				this.reader = new ConfigurationClassBeanDefinitionReader(
						registry, this.sourceExtractor, this.resourceLoader, this.environment,
						this.importBeanNameGenerator, parser.getImportRegistry());
			}
			this.reader.loadBeanDefinitions(configClasses);//会对configuration class内的bean进行注册
...

```


## @Resource的实现
### 使用例子
```$xslt
//task
package com.example.demo.service;

public interface Task {

    void doTask(String taskName);
}

//taskImpl
package com.example.demo.service;

import org.springframework.stereotype.Service;

@Service
public class TaskImpl implements Task {

    @Override
    public void doTask(String taskName) {
        System.out.println(taskName);
    }
}

//controller
package com.example.demo.controller;

import com.example.demo.service.Task;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import javax.annotation.Resource;

@RestController
public class TestController {

    @Resource
    Task task;

    public TestController() {
        System.out.println("a");
    }


    @GetMapping("/hello")
    public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
        return String.format("Hello %s!", name);
    }

    @GetMapping("/echo")
    public String echo() {
        task.doTask("test");
        return "just fine";
    }

}

```

### 实际实现
```$xslt
//ioc过程
doCreateBean:559, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support) [2]
createBean:524, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
lambda$doGetBean$0:335, AbstractBeanFactory (org.springframework.beans.factory.support)
getObject:-1, 1079125839 (org.springframework.beans.factory.support.AbstractBeanFactory$$Lambda$325)
getSingleton:234, DefaultSingletonBeanRegistry (org.springframework.beans.factory.support)
doGetBean:333, AbstractBeanFactory (org.springframework.beans.factory.support)
getBean:208, AbstractBeanFactory (org.springframework.beans.factory.support)
resolveCandidate:276, DependencyDescriptor (org.springframework.beans.factory.config)
doResolveDependency:1380, DefaultListableBeanFactory (org.springframework.beans.factory.support)
resolveDependency:1300, DefaultListableBeanFactory (org.springframework.beans.factory.support)
autowireResource:521, CommonAnnotationBeanPostProcessor (org.springframework.context.annotation)
getResource:497, CommonAnnotationBeanPostProcessor (org.springframework.context.annotation)
getResourceToInject:650, CommonAnnotationBeanPostProcessor$ResourceElement (org.springframework.context.annotation)
inject:228, InjectionMetadata$InjectedElement (org.springframework.beans.factory.annotation)
inject:119, InjectionMetadata (org.springframework.beans.factory.annotation)
postProcessProperties:318, CommonAnnotationBeanPostProcessor (org.springframework.context.annotation)
populateBean:1413, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
doCreateBean:601, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support) [1]
createBean:524, AbstractAutowireCapableBeanFactory (org.springframework.beans.factory.support)
lambda$doGetBean$0:335, AbstractBeanFactory (org.springframework.beans.factory.support)
getObject:-1, 1079125839 (org.springframework.beans.factory.support.AbstractBeanFactory$$Lambda$325)
getSingleton:234, DefaultSingletonBeanRegistry (org.springframework.beans.factory.support)
doGetBean:333, AbstractBeanFactory (org.springframework.beans.factory.support)
getBean:208, AbstractBeanFactory (org.springframework.beans.factory.support)
preInstantiateSingletons:944, DefaultListableBeanFactory (org.springframework.beans.factory.support)
finishBeanFactoryInitialization:918, AbstractApplicationContext (org.springframework.context.support)
refresh:583, AbstractApplicationContext (org.springframework.context.support)
refresh:145, ServletWebServerApplicationContext (org.springframework.boot.web.servlet.context)
refresh:758, SpringApplication (org.springframework.boot)
refreshContext:438, SpringApplication (org.springframework.boot)
run:337, SpringApplication (org.springframework.boot)
run:1336, SpringApplication (org.springframework.boot)
run:1325, SpringApplication (org.springframework.boot)
main:20, DemoApplication (com.example.demo)
```
__说明__,在`TestController`的实例化过程，会处理依赖关系，其中发现通过`@Resource`依赖了`Task`；此时找到实例化的`TaskImpl`并提供给`TaskController`，
完成`@Resource`的注入
