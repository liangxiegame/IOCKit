# IOCKit
独立的 IOC/DI  Container，依赖注入、控制反转

由 QFramework 团队官方维护的独立工具包（不依赖 QFramework）。

## 环境要求

* Unity 2018.4LTS

## 安装

* PackageManager
    * add from package git url：https://github.com/liangxiegame/IOCKit.git 
    * 或者国内镜像仓库：https://gitee.com/liangxiegame/IOCKit.git
* 或者直接复制[此代码](IOCKit.cs)到自己项目中的任意脚本中

## 快速开始

```  csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using QFramework;

namespace QFramework.Example
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



## 更多

* QFramework 地址: https://github.com/liangxiegame/qframework
