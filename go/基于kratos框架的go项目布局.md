参考学习文章——
https://go-kratos.dev/blog/go-project-layout

kratos中一个典型的go项目布局
application
|____api
| |____helloworld
| | |____v1                  //用于存放protobuf生成的.proto文件和相关文件，.proto文件通常描述对外的接口，入参，出参等信息
| | |____errors
|____cmd
| |____helloworld           //项目的入口，main文件存放处
|____configs                //yaml配置文件
|____internal               //主要内部代码
| |____conf                 //可以存放.proto配置文件，用于读取yaml文件中的数据
| |____data                 //用于数据库交互，且把从数据库中获取到的数据，转换为业务对象，传到biz层
| |____biz                  //用于处理业务的主要逻辑，定义repository接口，获取data层数据
| |____service              //实现对外访问系统的接口，是客户端访问系统的入口，主要用于请求分发，不做过多的逻辑处理。通常函数名和v1下.proto文件中的一致
| |____server               //创建和配置 HTTP 和 gRPC 服务实例。注册对应的 service，使其对外提供服务。将协议相关的配置（如 HTTP、gRPC）与业务逻辑解耦。
|                           ---保证服务启动和协议配置可以独立管理，便于后期维护和扩展。
|____test                   //用于测试
|____pkg                    //外部应用程序可以使用的库代码
|____go.mod                 //模块管理文件，用于管理依赖项，模块版本相关信息
|____go.sum                 //和go.mod搭配使用，记录每个依赖的加密哈希值，以保证依赖的正确性和安全性。
|____LICENSE                //定义代码使用、修改、分发和共享的条款的文件
|____README.md              //项目说明文件