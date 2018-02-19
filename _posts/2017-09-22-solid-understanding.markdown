---
layout: splash
title: "Understanding of SOLID"
date:   2017-09-22 12:06:46 +0800
categories: java
comments: false
share: true
published: true
---

## Brief

S|The Single Responsibility Principle | SRP
O|The Open／Closed Principle | OCP
L|The Liskov Substitution Principle | LSP
I|The Interface Segregation Principle | ISP
D|The Dependency Inversion Principle | DIP

<br />

## Details 

### S for Single Responsibility Principle
The single responsibility principle (SRP) asserts that a class or module should do one thing only. If need the class do more things, seperate it into two.


### O for Open／Closed Principle
Open/Closed Principle (OCP) states that software entities should be *open for extension*, but *closed for modification*.
Sample as below, every time add/modify a payment type, need modify the class. it is not a good way.
```java
// Open／Closed Principle - Bad example
public class PayHandler {
    public Result<T> pay(Param param) {
        if(param.getType() == "ALIPAY") {
            // Handle Alipay
            ...
        } else if(param.getType() == "WeChatPay") {
           // Handle WeChatPay
           ...
        }
    }
}
```

Better way as below:
```java
// Open／Closed Principle - Good example
public class PayHandler {
    private Map<String, PayProcessor> processors;
    public Result<T> pay(Param param) {
        PayProcessor payProcessor = processors.get(param.getType());
        return payProcessor.handle(param);
    }
}

interface PayProcessor {
    Result<T> handle(Param param);
}

public class AlipayProcessor implements PayProcessor {
    ...
}

public class WeChatPayProcessor implements PayProcessor {
    ...
}
```
We only need to modify the target payment processor when there is a modification requirement.
### L for Liskov Substitution Principle
Liskov Substitution Principle (LSP) states that every subclass/derived class should be substitutable for their base/parent class.
Explain: a Lorry class is subclass of Car class, as Car can drive, Lorry also can drive.
It is defined in Java language grammar already.

### I for Interface Segregation Principle
Many client specific interfaces are better than one general purpose interface.
Sample as below, as WeChat don't have the refund function.
```java
// Interface Segregation Principle - Bad example
interface PayChannel {
    void charge();
    void refund();
}

class AlipayChannel implements PayChannel {
    public void charge() {
        ...
    }
    public void refund() {
        ...
    }
}

class WeChatChannel implements payChannel {
    public void charge() {
        ...
    }
    public void refund() {
        // Not used !!!
    }
}
```

Better way as below:
```java
// Interface Segregation Principle - Good example
interface PayChannel {
    void charge();
}

interface RefundableChannel {
     void refund();
}

class AlipayChannel implements PayChannel, RefundableChannel {
    public void charge() {
        ...
    }
    public void refund() {
        ...
    }
}

class WeChatChannel implements PayChannel {
    public void charge() {
        ...
    }
}
```

### D for Dependency Inversion Principle
Depend upon Abstractions. Do not depend upon concretions.
```java
// Dependency Inversion Principle - Good example
iinterface PayChannel {
    void charge();
}

class WeChatChannel implements PayChannel {
    public void charge() {
        ...
    }
}

class Shop {
    PayChannel payChannel;

    public void setPayChannel(PayChannel w) {
        payChannel = w;
    }

    public void makePayment() {
        payChannel.pay();
    }
}
```


