原文链接：[http://www.tutorialspoint.com/design_pattern/business_delegate_pattern.htm](http://www.tutorialspoint.com/design_pattern/business_delegate_pattern.htm)
业务代理模式经常用来解耦表现层和业务层。通常用来减少沟通或在表现层的代码中远程查询业务层中的功能。在业务层中有以下几个实体。

- Client（客户端） - 表现层代码，可能是 JSP，Servlet 或者是 Java UI 代码。
- Business Delegate（业务代理） - 为客户端实体类访问业务服务方法提供了一个唯一的入口点。
- Lookup Service （查询服务） - 查询服务对象负责获取相关的业务实现和提供业务对象访问业务代码对象。
- Business Service （业务服务） - 业务服务接口。会有具体的类来实现这个业务接口，提供真正的业务实现逻辑。 

### 实现
我们将会创建一个 Client，BusinessDelegate，BusinessService，LookupService，JMSService 和 EJBService 来代表业务代理模式中的各种实体。

### 第一步
创建 BusinessService 接口

BusinessService.java

    public interface BusinessService {
        public void doProcessing();
    }
    
### 第二步
创建具体的服务类

EJBService.java

    public class EJBService implements BusinessService {
        @Override
        public void doProcessing() {
            System.out.println("Processing task by invoking EJB Service");
        }
    }
    
JMSService.java
    
    public class JMSService implements BusinessService {
        @Override
        public void doProcessing() {
            System.out.println("Processing task by invoking EJB Service");        
        }
        
    }
        
### 第三步
创建业务查询服务

    public class BusinessLookup {
        public BusinessService getBusinessService(String serviceType) {
            if (serviceType.equalsIgnoreCase("EJB")) {
                return new EJBService();
            } else {
                return new JMSService();
            }
        } 
    } 

### 第四步
创建业务代理
BusinessDelegate.java

    public class BusinessDelegate {
        private BusinessLookup lookupService = new BusinessLookup();
        private BusinessService businessService;
        private String serviceType;
        
        public setServiceType(String serviceType) {
            this.serviceType = serviceType;
        }
        
        public void doTask() {
            businessService = lookupService.getBusinessService(serviceType);
            businessService.doProcessing();
        }
    }
    
第五步
创建 Client（客户端）
Client.java
    
    public class Client {
        BusinessDelegate businessService;
        
        public Client(BusinessDelegate businessDelegate) {
            this.businessDelegate = businessDelegate;
        }
        
        public void doTask() {
            businessService.doTask();
        }
    }
第六步
使用 BusinessDelegate 和 Client 来演示业务代理模式
BusinessDelegatePatternDemo.java
    
    public class BusinessDelegatePatternDemo {
        public void main(String[] args) {
            BusinessDelegate businessDelegate = new BusinessDelegate();
            businessDelegate.setServiceType("EJB");
            
            Client client = new Client(businessDelegate);
            client.doTask();
            
            businessDelegate.setServiceType("JMS");
            client.doTask();
        }
    }
第七步
验证输出。
    
    Processing task by invoking EJB Service.
    Processing task by invoking JMS Service.
    
          
    
