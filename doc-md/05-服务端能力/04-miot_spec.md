<a name="module_miot/service/spec"></a>

## miot/service/spec
主要面向的是支持Spec协议的设备， 通过提供的API可以实现与设备之间进行通信等功能;
该模块提供的能力大致如下:
1、获取设备的Spec信息  2、获取或修改设备的属性值  3、请求调用设备的方法

**Export**: public  
**Doc_name**: miot_spec  
**Doc_index**: 4  
**Doc_directory**: service  
**Example**  
```js
import { Service } from "miot";
Service.spec.getSpecString(xxx).then(res => {
 console.log("res", res)
}).catch(error => {
   console.log("error", error)
});
```

* [miot/service/spec](#module_miot/service/spec)
    * [~ISpec](#module_miot/service/spec..ISpec)
        * [.getPropertiesValue(params, datasource)](#module_miot/service/spec..ISpec+getPropertiesValue) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
        * [.setPropertiesValue(params)](#module_miot/service/spec..ISpec+setPropertiesValue) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
        * [.doAction(params)](#module_miot/service/spec..ISpec+doAction) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
        * [.reportPropChanged(params)](#module_miot/service/spec..ISpec+reportPropChanged) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
        * [.getSpecString(did)](#module_miot/service/spec..ISpec+getSpecString) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
        * [.getCurrentSpecValue(did)](#module_miot/service/spec..ISpec+getCurrentSpecValue) ⇒


* * *

<a name="module_miot/service/spec..ISpec"></a>

### miot/service/spec~ISpec
**Kind**: inner interface of [<code>miot/service/spec</code>](#module_miot/service/spec)  

* [~ISpec](#module_miot/service/spec..ISpec)
    * [.getPropertiesValue(params, datasource)](#module_miot/service/spec..ISpec+getPropertiesValue) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
    * [.setPropertiesValue(params)](#module_miot/service/spec..ISpec+setPropertiesValue) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
    * [.doAction(params)](#module_miot/service/spec..ISpec+doAction) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
    * [.reportPropChanged(params)](#module_miot/service/spec..ISpec+reportPropChanged) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
    * [.getSpecString(did)](#module_miot/service/spec..ISpec+getSpecString) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
    * [.getCurrentSpecValue(did)](#module_miot/service/spec..ISpec+getCurrentSpecValue) ⇒


* * *

<a name="module_miot/service/spec..ISpec+getPropertiesValue"></a>

#### iSpec.getPropertiesValue(params, datasource) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
请求获取设备的属性值； 由于是发起网络请求，数据的正确性可以通过抓包来查看；
只要网络请求成功会代码会执行到then（与具体是否获取到设备属性值无关）， 网络请求失败则会执行到catch
code 具体表示什么意思可以查看： https://iot.mi.com/new/doc/05-米家扩展程序开发指南/05-功能接口/06-MIOT-Spec.html

**Kind**: instance method of [<code>ISpec</code>](#module_miot/service/spec..ISpec)  
**Returns**: <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code> - 成功时分两种情况：
获取设备属性成功时： [{"did":"xxx","siid":x,"piid":x,"code":0，value: xxx },……]
获取设备属性失败时： [{"did":"xxx","siid":x,"piid":x,"code":xxx},……]
失败时：{code:xxx, message:xxx}  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| params | <code>Array</code> |  | [{did: 1, siid: 1, piid: 1},{did: 1, siid:2, piid: 3},……] |
| datasource | <code>int</code> | <code>1</code> | 从10036开始增加datasource，可不传（不传的默认dataSource=1）,dataSource可选值如下: datasource=1  优先从服务器缓存读取，没有读取到下发rpc；不能保证取到的一定是最新值 datasource=2  直接下发rpc，每次都是设备返回的最新值 datasource=3  直接读缓存;没有缓存的 code 是 -70xxxx；可能取不到值 后台的默认策略是datasource=3；开发者可根据需求特性选择dataSource的值，如果对实时性要求不高，建议dataSource=1或者dataSource=3,以减轻后台服务的压力 |


* * *

<a name="module_miot/service/spec..ISpec+setPropertiesValue"></a>

#### iSpec.setPropertiesValue(params) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
请求设置设备的属性值，由于是发起网络请求，数据的正确性可以通过抓包来查看；
只要网络请求成功会代码会执行到then（与具体是否获取到设备属性值无关）， 网络请求失败则会执行到catch
code 具体表示什么意思可以查看： https://iot.mi.com/new/doc/05-米家扩展程序开发指南/05-功能接口/06-MIOT-Spec.html

**Kind**: instance method of [<code>ISpec</code>](#module_miot/service/spec..ISpec)  
**Returns**: <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code> - 成功时分两种情况：
设置设备属性成功时：  [{"did":"xxx","siid":x,"piid":x,"code":0 },……]
设置设备属性失败时：  [{"did":"xxx","siid":x,"piid":x,"code":xxx },……]
失败时：{code:xxx, message:xxx}  

| Param | Type | Description |
| --- | --- | --- |
| params | <code>Array</code> | [{did: 1, siid: 1, piid: 1, value:'any'},{did: 1, siid:2, piid: 3, value: 'any'},……] |


* * *

<a name="module_miot/service/spec..ISpec+doAction"></a>

#### iSpec.doAction(params) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
请求调用设备的方法,由于是发起网络请求，数据的正确性可以通过抓包来查看；
只要网络请求成功会代码会执行到then（与具体是否获取到设备属性值无关）， 网络请求失败则会执行到catch
code 具体表示什么意思可以查看： https://iot.mi.com/new/doc/05-米家扩展程序开发指南/05-功能接口/06-MIOT-Spec.html

**Kind**: instance method of [<code>ISpec</code>](#module_miot/service/spec..ISpec)  
**Returns**: <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code> - 成功时分两种情况：
方法执行成功时：  {"did":"xxx","siid":x,"piid":x,"code":0 }
方法执行失败时：  {"did":"xxx","siid":x,"piid":x,"code":xxx }
失败时：{code:xxx, message:xxx}  

| Param | Type | Description |
| --- | --- | --- |
| params | <code>JSON</code> | {did: action.did, siid: action.siid, aiid: action.iid, in: action.params},其中，action.params为数组。例如 {did: 1, siid: 1, aiid: 1, in: [17,"shanghai"]} |


* * *

<a name="module_miot/service/spec..ISpec+reportPropChanged"></a>

#### iSpec.reportPropChanged(params) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
该接口用来上报设备属性，一般供蓝牙设备使用

**Kind**: instance method of [<code>ISpec</code>](#module_miot/service/spec..ISpec)  
**Returns**: <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code> - {"results": [{"did": "xxx", "siid": 1, "piid": 1, "code": 0}]}  
**Since**: SDK10045  

| Param | Type | Description |
| --- | --- | --- |
| params | <code>JSON</code> | {"props": [{"did": "xxx", "siid": 1, "piid": 1, "value": "xxx(参考spec定义的类型设置)", "tid": 123(与网关接口定义一致)}], "version": ""} |


* * *

<a name="module_miot/service/spec..ISpec+getSpecString"></a>

#### iSpec.getSpecString(did) ⇒ <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code>
获取设备的spec详情, 由于是发起网络请求，数据的正确性可以通过抓包来查看；
只要网络请求成功会代码会执行到then（与具体是否获取到设备属性值无关）， 网络请求失败则会执行到catch

**Kind**: instance method of [<code>ISpec</code>](#module_miot/service/spec..ISpec)  
**Returns**: <code>[ &#x27;Promise&#x27; ].&lt;JSON&gt;</code> - 设备的Spec属性详情
方法执行成功时：直接返回设备具体内容，json结构字符串
失败时：{code:xxx, message:xxx}  

| Param | Description |
| --- | --- |
| did | 设备的did |


* * *

<a name="module_miot/service/spec..ISpec+getCurrentSpecValue"></a>

#### iSpec.getCurrentSpecValue(did) ⇒
刚进入插件时，如果需要获取米家APP缓存的设备的miot-spec数据，则调用此方法获取，有可能没有数据,不建议使用
注意调用方法的时候，方法要加上async
使用方式：let data = await Service.spec.getCurrentSpecValue(did);

**Kind**: instance method of [<code>ISpec</code>](#module_miot/service/spec..ISpec)  
**Returns**: 缓存的设备的miotSpec属性，
方法执行成功时,Android iOS返回数据格式不一样
Android：string类型, {"code":0, "result":"[]"} or {"code":0, "result":"[{"did":"xxx","siid":x,"piid":x,"code":0 }, ...]"}
iOS： 返回值同上面的getPropertiesValue方法。此方法只返回code为0（get成功）的数据  
**Since**: 10003  

| Param | Description |
| --- | --- |
| did | 设备的did，必传 |


* * *

