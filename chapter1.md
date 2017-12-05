### API接口文档生成工具的使用方法

## 1、在工程中引如相关包

`<dependency>`

`<groupId>com.weahan.utility</groupId>`

`<artifactId>smile-apiGenerator</artifactId>`

`<version>1.1.0-SNAPSHOT</version>`

`</dependency>`

注：继承自下面以上版本pom的工程，已经自动依赖引入，无需再次引入：

`<parent>`

`<groupId>com.weahan.core</groupId>`

`<artifactId>weahan-core-provider</artifactId>`

`<version>1.1.4</version>`

`</parent>`

## 2、给代码添加相应注解

### 2.1 添加类注解

在需要生成API文档的类上添加如下注解：

```java
@Tag("疾病服务")
public class DiseasePlusService{

}
```

@Tag里面的内容为此服务的名称。

### 2.2 添加接口方法注解

在需要生成API文档的接口方法上添加如下注解，以下是范例：

```java
@Description\({

        "jsonString=searchInput=String=icd-10编码\(疾病名称\)&lt;/br&gt;" +

                "choice=String=疾病分类&lt;/br&gt;" +

                "dataStatus=tinyint=数据状态&lt;/br&gt;",

        "result=查询结果对象",

        "result.rows=数据集",

        "result.total=条数",

        "result.code=查询结果代码",

        "result.message=操作结果描述"

        }\)

@Example\({

        "jsonString={\"searchInput\":\"糖尿病\",\"choice\":\"免疫系统疾病\",\"dataStatus\":1}",

        "result={\"total\":2,\"code\":200,\"message\":\"查询成功\"}",

        "result.rows=",

        "result.total=18",

        "result.code=200",

        "result.message=查询成功"

        }\)

@Required\("jsonString"\)

@Excludes\({ "" }\)

@Path\(value = "/disease/list", description = "查询疾病字典"\)

@GetMapping\("/disease/list"\)

public ResultLogic getDiseaseList\(@RequestParam final String jsonString\) {
}
```

## 3、添加生成工具类

在工程里增加生成工具类，并根据含义进行配置，如下所示：

`package com.weahan.platform.services;`

`import java.util.Calendar;`

`import com.sunx.api.common.Config;`

`import com.sunx.api.main.Generator;`

`import com.sunx.api.model.InfoDescription;`

`/**`

`*`

`*/`

`public class GenApiApplication {`

`public static void main(String[] args) {`

`InfoDescription info = new InfoDescription();`

`info.setTitle("疾病服务");`

`info.setDescription("疾病服务接口说明");`

`info.setVersion("v1.0.0");`

`info.setHost("api.weahan.com");`

`info.setBasePath("/diseaseService");`

`info.setEmail("api@weahan.com");`

`info.setTermsOfService("aurora");`

`info.setGit("git.com/weahan");`

`info.setDate(Calendar.getInstance().getTime());`

`String[] servPacks = { "com.weahan.platform.services.diseaseService**" };`

`// 默认：result`

`// Config.responseParamName = "data";`

`// 默认："E:\\api-generator\\api.js"`

`Config.apiFilePath = "E:\\space_node\\smile-apidoc\\api.js";`

`Generator.generatorApi(info, servPacks);`

`}`

`}`

