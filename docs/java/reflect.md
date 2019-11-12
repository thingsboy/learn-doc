# 反射



# 反射示例

User.java

```java
package com.sunrizetech.bean;

public class User {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

Test.java

```java
public class Test {

  public static void main(String[] args) {
    Class clz = Class.forName("com.sunrizetech.bean.User");
    User user = (User) clz.newInstance();
    
    Method setMethod = clz.getMethod("setName", String.class);
    setMethod.invoke(user, "名字");
    
    Method getMethod = clz.getMethod("getName");
    getMethod.invoke(user);
  }
}
```





