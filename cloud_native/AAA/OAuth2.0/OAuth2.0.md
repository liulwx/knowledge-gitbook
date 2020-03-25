# What?
-----------------------------------------------------------
>The OAuth 2.0 authorization framework enables a third-party
   application to obtain limited access to an HTTP service, either on
   behalf of a resource owner by orchestrating an approval interaction
   between the resource owner and the HTTP service, or by allowing the
   third-party application to obtain access on its own behalf.  This
   specification replaces and obsoletes the OAuth 1.0 protocol described
   in RFC 5849.

说白了就是OAuth 2.0是一个授权框架，最多的用处是授予第三方的应用以用户（已经在系统中存在的）的身份获取某种资源的权限。你需要牢记的是OAuth2.0仅仅是一个授权(authorization)系统。有关认证(authentication)的事情不是OAuth2.0所需要做的，有其他的东西会做(OpenID connect)，我们之后会提到。
## 什么时候你需要使用OAuth 2.0 
OAuth 2.0是一个授权框架，而且还是一个相对比较复杂的授权框架。正如引用里所描述，你需要使用的场景是期望你的系统的资源可以以某种安全的方式暴露给第三方的应用。

##### 举个例子（坏的做法）
在没有OAuth2.0之前，如果某个程序想要获得其他系统中用户的一些权限，他需要怎么做呢？ 假设有个**打折系统**的程序想要获取**毛毛鸭**在**淘宝**的消费记录来方便针对**毛毛鸭** 制定一些策略。他可能需要在某个界面要求**毛毛鸭** 填写他的**淘宝**账号和密码，然后给出一些bullshit的解释（我们保证不会乱用您的密码，保证不会泄露您的密码），如果你了解过撞库攻击或者其他安全方面的一些知识，你就知道他们的做法有多么的不安全。
没错OAuth2.0就是为了避免这种不安全的授权方式(直接将用户名，密码给到第三方)，而产生的一种安全的授权框架

## OAuth 2.0重要的术语
OAuth2.0之所以理解起来比较绕，就是因为他定义了很多奇奇怪怪的术语，如果无法对这些术语进行充分的了解，是无法真正理解OAuth 2.0的奥秘的。
#### 角色
OAuth2.0一定定义了4种角色

* Resource Owner
   - 是一个可以授予被保护资源权限的实体。可以是个人，也可以是其他东西。如果是个人的话，我们叫他end-user。 我们坏例子里面的**毛毛鸭**
* Resource Server
   - 是一个实际可以提供被保护资源的服务。他可以通过验证access token（我们之后会解释）来提供被保护的资源。我们例子里的**淘宝**里面托管淘宝消费记录的服务
* Client
   - 得到了Resource Owner授权可以以Resource Owner身份获取被保护的资源（**上个例子里的淘宝消费记录**）的App。他不代表任何特定的实现特征（server， desktop，devices都可以）
* Authorization server
   - 是一个在成功认证(authentication)resource owner身份，并且获取了Resource owner授权后将access token发送给client的服务