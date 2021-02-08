# SpringBoot核心原理分析

## 一、常用注解

### **1、@SpringBootApplication** 

```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration->@Configuration //重点分析1
@EnableAutoConfiguration //重点分析2
@ComponentScan( //重点分析3
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication {
    @AliasFor(
        annotation = EnableAutoConfiguration.class
    )
    Class<?>[] exclude() default {};

    @AliasFor(
        annotation = EnableAutoConfiguration.class
    )
    String[] excludeName() default {};

    @AliasFor(
        annotation = ComponentScan.class,
        attribute = "basePackages"
    )
    String[] scanBasePackages() default {};

    @AliasFor(
        annotation = ComponentScan.class,
        attribute = "basePackageClasses"
    )
    Class<?>[] scanBasePackageClasses() default {};
}
```

由上源码可知**@SpringBootApplication**是一个符合注解，相当于以下

- **@SpringBootConfiguration->@Configuration //重点分析1**
- **@EnableAutoConfiguration //重点分析2**
- **@ComponentScan //重点分析3**

这三个注解将后面给大家详细展开分析。

### 2、@ComponentScan 

```java
@ComponentScan(basePackages = "com.your.package")
public class ConfigurationMain {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(ConfigurationMain.class);
        //获取容器中的所有bean的元数据
        String[] defNames = applicationContext.getBeanDefinitionNames();
        for(int i=0;i<defNames.length;i++){
            String defName = defNames[i];
            System.out.println(defName);
            Object bean = applicationContext.getBean(defName);
            System.out.println(bean);
        }
    }
}
```

上面代码可知：@ComponentScan(basePackages = "com.your.package")是用来置顶容器启动时需扫描的包，在这个指定的包下所有的@Service、@Controller、@Repository、@Configuration等组件将杯初始化。

如果想在SpringBoot启动的时候，能够扫到不在默认范围包的路径可以如下操作。

```java
@SpringBootApplication(scanBasePackages = {"你需要额外扫包的路劲"})
public class SpringBootFirstApplication {
    public static void main(String[] args) {
        //这里大家就清楚了为什么启动的时候会传入SpringBootFirstApplication.class。
        //Spring为了在启动的过程，可以通过SpringBootFirstApplication.class获取一些前置配置条件。
        SpringApplication.run(SpringBootFirstApplication.class);
    }
}
//其实@SpringBootApplication中对ComponentScan进行了参数绑定。
    @AliasFor(
        annotation = ComponentScan.class,
        attribute = "basePackages"
    )
    String[] scanBasePackages() default {};
```



### 3、@Configuration

```java
public class SecondMain {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext applicationContext=new
                      //SpringConfig.class自定义的一个@Configuration注解类
                      AnnotationConfigApplicationContext(SpringConfig.class);
        String[] defNames=applicationContext.getBeanDefinitionNames();
        for(int i=0;i<defNames.length;i++){
            System.out.println(defNames[i]);
        }
    }
}
```

- **SpringConfig.class**

  ```java
  @Import(OtherConfig.class)//下面具体会将@Import用法
  @Configuration
  public class SpringConfig {
      @Bean
      public DefaultBean defaultBean(){
          return new DefaultBean();
      }
  }
  ```

- **OtherConfig.class**

  ```java
  @Configuration
  public class OtherConfig {
      /**
       * org.springframework.beans.factory.support.DefaultSingletonBeanRegistry
       * singletonObjects //bean容器
       */
      @Bean
      public OtherBean otherBean(){
          //进行一些列自定义初始化
          OtherBean bean = new OtherBean();
          bean.setName("testName");
          return bean;
      }
  }
  ```

- **OtherBean.class**

  ```java
  @Data //lombook
  public class OtherBean {
     private String name;
  }
  ```





### 4、@Import

> 第一种使用方式：
>
> 关联触发简单的Bean的初始化@Import(Test.class)，这样就可以在容器中找到类型为Test.class的实例了。
>
> 第二种使用方式：
>
> 关联触发@Configuration相关组件初始化@Import（TestConfiguration.class）。这样就可以在容器中找到TestConfiguration类中定义的一些Bean实例。
>
> 第三种使用方式：
>
> 关联扩展Spring相关的内部机制，下面结合Spring常用的两个例子给大家扩展理解。

- **自定义一个注解 @EnableDefineService，模拟EnableAutoConfiguration 功能** 

  ```java
  @Target(ElementType.TYPE)
  @Retention(RetentionPolicy.RUNTIME)
  @Documented
  @Inherited
  @Import(
      {
          CacheImportSelector.class, //扩展一
          LoggerDefinitionRegistrar.class //扩展二
      }
  ) 
  public @interface EnableDefineService {
      //配置一些方法
      Class<?>[] exclude() default {};
  }
  ```

- **CacheImportSelector.class**

  ```java
  public class CacheImportSelector implements ImportSelector {
      @Override
      public String[] selectImports(AnnotationMetadata annotationMetadata) {
          Map<String,Object> attributes=               annotationMetadata.getAnnotationAttributes(EnableDefineService.class.getName());
          /**
            * annotationMetadata可以获取启动类上所有的注解元数据进行操作
            * 动态注入bean :自己去实现判断逻辑实现动态配置
            */
           //返回的是一个固定的CacheService
          return new String[]{CacheService.class.getName()}; 
      }
  }
  ```

- **LoggerDefinitionRegistrar.class**

  - **应用一  手动塞入Bean到Spring容器中。**

    ```java
    public class LoggerDefinitionRegistrar implements ImportBeanDefinitionRegistrar {
        @Override
        public void registerBeanDefinitions(AnnotationMetadata annotationMetadata, BeanDefinitionRegistry beanDefinitionRegistry) {
            Class beanClass = LoggerService.class;
            RootBeanDefinition beanDefinition = new RootBeanDefinition(beanClass);
            String beanName = StringUtils.uncapitalize(beanClass.getSimpleName());
            //手动加入Bean到Spring容器中。
            beanDefinitionRegistry.registerBeanDefinition(beanName,beanDefinition);
        }
    }
    ```

  - **应用二 对容器中初始化的Bean进行再次改造，下面就以自定义加载配置环境为例。**

    ```java
    public class PropertySourceDetectorConfiguration implements ImportBeanDefinitionRegistrar {
    
        private static final String PATH_PREFIX = "profiles";
    
        @Override
        public void registerBeanDefinitions(AnnotationMetadata importingClassMetadata, BeanDefinitionRegistry registry) {
            //获取Bean工厂
            DefaultListableBeanFactory beanFactory = (DefaultListableBeanFactory) registry;
            //获取ConfigurableEnvironment，此时容器中该Bean已初始化了。但是我们需要塞进自己的配置类，所以需要拿到已初始化完成的获取ConfigurableEnvironment进行操作。
            ConfigurableEnvironment environment = beanFactory.getBean(ConfigurableEnvironment.class);
            List<AbstractPropertySourceDetector> propertySourceDetectors = new ArrayList<>();
            //收集所有AbstractPropertySourceDetector的实现类，后续处理不同的profile遍历用到
            configurePropertySourceDetectors(propertySourceDetectors, beanFactory);
            //装载所有的子类
            PropertySourceDetectorComposite propertySourceDetectorComposite = new PropertySourceDetectorComposite();
            propertySourceDetectorComposite.addPropertySourceDetectors(propertySourceDetectors);
            //获取当前激活的profile：dev、test等等
            String[] activeProfiles = environment.getActiveProfiles();
            ResourcePatternResolver resourcePatternResolver = new PathMatchingResourcePatternResolver();
            try {
                for (String profile : activeProfiles) {
                    String location = PATH_PREFIX + File.separator + profile + File.separator + "*";
                    /**
                     * 读取classpath下某个目录下的所有文件。
                     */
                    Resource[] resources = resourcePatternResolver.getResources(location);
                    for (Resource resource : resources) {
                        propertySourceDetectorComposite.load(environment, resource.getFilename(), resource);
                    }
                }
            } catch (IOException e) {
                throw new IllegalStateException(e);
            }
        }
    
        private void configurePropertySourceDetectors(List<AbstractPropertySourceDetector> propertySourceDetectors, DefaultListableBeanFactory beanFactory) {
            Map<String, AbstractPropertySourceDetector> beansOfType = beanFactory.getBeansOfType(AbstractPropertySourceDetector.class);
            for (Map.Entry<String, AbstractPropertySourceDetector> entry : beansOfType.entrySet()) {
                propertySourceDetectors.add(entry.getValue());
            }
            propertySourceDetectors.add(new JsonPropertySourceDetector());
            propertySourceDetectors.add(new YamlPropertySourceDetector());
            propertySourceDetectors.add(new PropertiesPropertySourceDetector());
        }
    }
    ```

    

​            

## 二、SpringBoot SPI机制

> SpringBoot SPI可以实现类似SpringBoot的starter插件。这里就不过多分析SPI原理了，不清楚的同学可以百度了解一下。关于这个分析网上有很多例子，这里就记录一下本人学习的实操的一个例子吧。实际演练过程需要创建两个工程下面就叫A、B工程。

- **A工程 **

  > **A**工程就相当于咋们平时手头负责的项目。只要通过maven引用依赖**B**工程就好了。
  >
  > 如果希望Spring帮我们自动加载**B**中的com.test.MyStarterConfig，就需要根据
  >
  > spring-autoconfigure-metadata.properties中定义的条件，创建相关的类文件。
  >
  > 这里就有个条件com.test.TestClass需要创建，否则com.test.MyStarterConfig是
  >
  > 不会被加载的。

- **B工程 类似于SpringBoot中的starter工程**

  在当前工程的resources目录下创建目录：META-INF，在这个目录下创建两个文件

  - resources
    - META-INF
      - spring.factories   文件1
      - spring-autoconfigure-metadata.properties 文件2

  

  - spring.factories 用于Spring的SPI机制帮忙自动加载**B**工程里面的com.test.MyStarterConfig。

    ```properties
    org.springframework.boot.autoconfigure.EnableAutoConfiguration= \
    com.test.MyStarterConfig
    ```

  - spring-autoconfigure-metadata.properties 用于starter启动条件控制。

    ```properties
    com.test.MyStarterConfig.ConditionalOnClass=com.test.TestClass
    ```

    >  上面的意思是当我们上面的**A**工程依赖**B**工程的时候。在**A**工程classpath下找不到com.test.TestClass类则Spring就不帮我们加载com.test.MyStarterConfig。反之就会帮我们加载com.test.MyStarterConfig，也就意味着com.test.MyStarterConfig中定义的Bean就会被初始化，放入Spring的容器中一遍后续咋们可以用。

  - com.test.TestClass

    ```java
    @Configuration
    public class MyStarterConfig {
        @Bean
        public MyUtil myUtil(){
            return new MyUtil();
        }
    }
    ```

  - com.test.MyUtil

    ```java
    public class MyUtil {
        public String study(){
            System.out.println("欢迎使用我开发的工具");
            return "欢迎使用我开发的工具";
        }
    }
    ```

  























