# QFramework.IOC
独立的 IOC/DI  Container，依赖注入、控制反转

## 快速开始

```  csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using QFramework;

namespace QF.Master.Example
{    

    public class ServiceA
    {
        public void Say()
        {
            Debug.Log("I am ServiceA:" + this.GetHashCode());
        }
    }
    
    public interface IService
    {
        void Say();
    }
  
    public class ServiceB : IService
    {
        public void Say()
        {
            Debug.Log("I am ServiceB:" + this.GetHashCode());
        }
    }
    
    public class ServiceC : IService
    {
        public void Say()
        {
            Debug.Log("I am ServiceC:" + this.GetHashCode());
        }
    }
  
    public class IOCExample : MonoBehaviour 
    {
        // 声明为需要注入的对象
        [Inject] 
        public ServiceA A {get;set;}

        [Inject] 
        public IService B {get;set;}

        [Inject] 
        public ServiceC C {get;set;}
        
        void Start () 
        {
            // 创建实例容器
            var container = new QFrameworkContainer();

            // 注册类型
            container.Register<ServiceA>();
            
            container.Register<IService,ServiceB>();

            container.RegisterInstance(new ServiceC());

            // 注入对象（会自动查找 Inject Atrributet的对象)
            container.Inject(this);

            // 注入之后，就可以直接使用 A 对象了
            A.Say();        
        }
    }
}
```

