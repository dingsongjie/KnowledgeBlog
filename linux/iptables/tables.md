---
description: iptables里的表
---

# tables

{% tabs %}
{% tab title="nat" %}
#### 使用场景

一般用来做网络地址转换

#### 可以使用的链

* prerouting
* input
* output
* postrouting

#### 查看table

iptables -t nat -L \[chain]
{% endtab %}

{% tab title="Second Tab" %}
####

#### 使用场景

一般用来做网络地址转换

#### 可以使用的链

* prerouting
* input
* output
*   postrouting

    #### 使用场景

    一般用来做网络地址转换

    #### 可以使用的链

    * prerouting
    * input
    * output
    * postrouting
{% endtab %}
{% endtabs %}
