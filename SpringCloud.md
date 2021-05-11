

#### 服务注册中心

##### Eureka

- 服务注册:@EnableEurekaServer或者@EnableDiscoveryClient
- 服务消费:@EnableEurekaClient

##### Zookeeper

#### 负载均衡

##### Ribbon(客户端)

- 负载均衡:@LoadBalancedf

- 使用这个标签后,可以使用从注册中心拿到的微服务接口,给予负载均衡的能力,默认使用已经实现的轮询算法

```Java
@Configuration
public class ApplicationContextConfig
{
    @Bean
    @LoadBalanced
    public RestTemplate getRestTemplate()
    {
        return new RestTemplate();
    }
}
```

- ribbon原理(轮询算法):

  ```Java
  public final  int getAndIncrement(){
      int next;
      int current;
      current = atomicInteger.get();
      do {
          next = current > Integer.MAX_VALUE ? 0 : current + 1;
      } while (!atomicInteger.compareAndSet(current, next));
      System.out.println("访问次数next:" + next);
      return next;
  }
  
  //负载均衡算法：rest接口第几次请求数 % 服务器集群总数量 = 实际调用服务器位置下标  ，每次服务重启动后rest接口计数从1开始。
  @Override
  public ServiceInstance instances(List<ServiceInstance> serviceInstances) {
  
      int index = getAndIncrement() % serviceInstances.size();
  
      return serviceInstances.get(index);
  }
  ```

#### 服务调用2

##### Feign

##### OpenFeign

#### 服务降级

##### Hystrix

##### resilience4j

#### 服务网关

##### Zuul

##### Zuul2

##### Gateway

#### 服务配置

##### Config

##### Nacos

#### 服务总线

##### Bus

##### Nacos