---
title: 聚合收银台支付
header: develop
nav: api
sidebar: open_payment
---
requestPolymerPayment
---
**版本：**swanjs 1.8.5 版本开始支持。

**解释：**百度聚合收银台，聚合了主流的百度钱包、微信、支付宝、网银等多种支付方式，方便开发者一站式快速接入多种支付渠道，让百度用户能在智能小程序场景下，直接完成支付、交易闭环，提升用户支付体验的同时，提高智能小程序的订单转化率。

了解更多信息，请查看 [百度电商开放平台：产品介绍](http://dianshang.baidu.com/platform/doclist/index.html#!/doc/nuomiplus_3_business/mini_program_cashier/product_intro.md)

**参数：**Object

**Object参数说明：**

|参数名 |类型  |必填  |说明|
|---- | ---- | ---- |---- |
|orderInfo| Object | 是 |订单信息|
|bannedChannels| StringArray | 否 | 需要隐藏的支付方式|
|success |Function  |  否  | 接口调用成功的回调函数|
|fail   | Function  |  否  | 接口调用失败的回调函数|
|complete  |  Function  |  否 |  接口调用结束的回调函数（调用成功、失败都会执行）|

**orderInfo 参数说明：**
- dealId: 跳转百度收银台支付必带参数之一，是百度收银台的财务结算凭证，与账号绑定的结算协议一一对应，每笔交易将结算到dealId对应的协议主体。
- appKey: 用以表示应用身份的唯一ID，在应用审核通过后进行分配，一经分配后不会发生更改，来唯一确定一个应用。
- totalAmount: 订单金额，单位为人民币分。
- tpOrderId: 商户平台自己记录的订单ID，当支付状态发生变化时，会通过此订单ID通知商户。
- dealTitle: 订单的名称。
- rsaSign: 对`appKey+dealId+tpOrderId`进行RSA加密后的密文，防止订单被伪造。签名过程见 [百度电商开放平台：签名与验签](https://dianshang.baidu.com/platform/doclist/index.html#!/doc/nuomiplus_2_base/sign_v2.md)
- bizInfo: 订单详细信息，需要是一个可解析为JSON Object的字符串。字段内容见： [百度电商开放平台：收银台接入](https://dianshang.baidu.com/platform/doclist/index.html#!/doc/nuomiplus_1_guide/beginner_v2/step3/cash.md)

**bannedChannels 参数说明：**

|channel |说明 |
|---- | ---- |
| Alipay | 支付宝 |
| BDWallet | 百度钱包 |
| WeChat | 微信支付|

**示例：**

```js
swan.requestPolymerPayment({
    orderInfo: {
        "dealId": "470193086",
        "appKey": "MMMabc",
        "totalAmount": "1",
        "tpOrderId": "3028903626",
        "dealTitle": "智能小程序Demo支付测试",
        "rsaSign": '',
        "bizInfo": ''
    },
    success: function (res) {
        swan.showToast({
            title: '支付成功',
            icon: 'success'
        });
    },
    fail: function (err) {
        swan.showToast({
            title: JSON.stringify(err)
        });
        console.log('pay fail', err);
    }
});
```