# 一、试用低代码引擎 Demo

## 访问地址

低代码引擎的 Demo 可以通过如下永久链接访问到：

[设计器 demo](https://lowcode-engine.cn/demo/demo-general/index.html)

# 二、低代码引擎 Demo环境搭建

## 环境准备

### Node

node 版本推荐 16.18.0。

#### 查看 Node 版本

![image.png](https://img.alicdn.com/imgextra/i4/O1CN01oCZKNz290LIu8YUTk_!!6000000008005-2-tps-238-70.png)

#### 通过 n 来管理 node 版本

可以安装 [n](https://www.npmjs.com/package/n) 来管理和变更 node 版本。

##### 安装 n

```bash
npm install -g n
```

##### 变更 node 版本

```bash
n 14.17.0
```


### 下载 Demo

可以前往 github（[https://github.com/alibaba/lowcode-demo](https://github.com/alibaba/lowcode-demo)）将 DEMO 下载到本地。

#### git clone

##### HTTPS

需要使用到 git 工具

```bash
git clone https://github.com/alibaba/lowcode-demo.git
```

### 选择一个 demo 项目

在 以 `demo-general` 为例：

```bash
cd demo-general
```

### 安装依赖

在 `lowcode-demo/demo-general` 目录下执行：

```bash
npm install
```

### 启动 demo

在 `lowcode-demo/demo-general` 目录下执行：

```bash
npm run start
```

之后就可以通过 [http://localhost:5556/](http://localhost:5556/) 来访问 DEMO 了。

# 三、低代码引擎Demo的使用
低代码编辑器中的区块主要包含这些功能点： ![image.png](https://img.alicdn.com/imgextra/i2/O1CN01aGQull1RVdGs7Pt6x_!!6000000002117-2-tps-3384-1784.png)


# 1. 分区块功能介绍

## 左侧：面板与操作区

### 物料面板

可以查找组件，并在此拖动组件到编辑器画布中 ![Dec-17-2021 19-12-46.gif](https://img.alicdn.com/imgextra/i1/O1CN01pEu7811SlwzxraLHG_!!6000000002288-1-tps-1468-754.gif)

### 大纲面板

可以调整页面内的组件树结构： ![Dec-17-2021 19-14-34.gif](https://img.alicdn.com/imgextra/i1/O1CN013DDLqt1GH0rAlajqi_!!6000000000596-1-tps-1468-754.gif) 可以在这里打开或者关闭模态浮层的展现： ![Dec-17-2021 19-19-18.gif](https://img.alicdn.com/imgextra/i2/O1CN01bQfS8W1JitokHRinC_!!6000000001063-1-tps-1468-754.gif)

### 源码面板

可以编辑页面级别的 JavaScript 代码和 CSS 配置 ![Feb-11-2022 14-51-59.gif](https://img.alicdn.com/imgextra/i1/O1CN01d11kK71Q223eWvL5F_!!6000000001917-1-tps-1532-614.gif)

### Schema 编辑

【开发者专属】可以编辑页面的底层 Schema 数据。 ![image.png](https://img.alicdn.com/imgextra/i3/O1CN01lcQOER23Q5sjA0Gn5_!!6000000007249-2-tps-3070-1648.png) 搭配顶部操作区的“保存到本地”和“重置页面”功能，可以实验各种 schema 对低代码页面的改变。

它们操作的数据关系是：

* 页面中的 Schema 数据：保存在低代码引擎中的 Schema，点击 Schema 面板中的“保存 Schema”时将修改引擎中的值，此外低代码引擎中的所有操作都可能修改到 Schema
* localStorage 数据：由“保存到本地”保存到 localStorage 中，页面初始化时将读取，预览页面时也会读取
* 默认 Schema：保存在 Demo 项目中的默认 Schema（`public/schema.json`），初始化页面时如果不存在 localStorage 数据即会读取，点击“重置页面”时，也会读取

# 2. 如何制作表格

## 步骤详解

### 拖入组件

一个常见的表格页面会包含查询框、表格和分页按钮。这些都在 Fusion UI 中进行了相应的封装，我们可以在左侧组件面板处找到他们。

![image.png](https://img.alicdn.com/imgextra/i2/O1CN01UU8pVT26XN1A0ExVG_!!6000000007671-2-tps-3032-1648.png)

将他们拖到画布之中： ![Feb-16-2022 16-58-59.gif](https://img.alicdn.com/imgextra/i3/O1CN01UAsQ8124HgDptzPrn_!!6000000007366-1-tps-1534-792.gif)

### 配置组件

选中刚拖入的“查询筛选”组件，您可以配置此组件： ![Feb-14-2022 17-59-47.gif](https://img.alicdn.com/imgextra/i2/O1CN01RiDUy31aufSeVk8IN_!!6000000003390-1-tps-1532-792.gif)

对于形如 Array 的配置项目，我们可以增删项目、修改常用项、修改顺序。

![image.png](https://img.alicdn.com/imgextra/i2/O1CN01eWOK0d1fOfsF9PZu9_!!6000000003997-2-tps-3060-1476.png)

掌握组件配置功能，我们就可以完成一个常用的查询框的配置： ![Feb-21-2022 18-05-52.gif](https://img.alicdn.com/imgextra/i1/O1CN0138fb0P1CTbHKWDBeo_!!6000000000082-1-tps-1532-790.gif)

### 绑定数据

低代码场景下，我们需要绑定动态的数据。通过左侧的源码编辑面板，我们可以创建动态数据和它的相关处理函数：

![image.png](https://img.alicdn.com/imgextra/i1/O1CN015Bw2aQ1jaMRWoYzv5_!!6000000004564-2-tps-2976-1478.png)

如图，我们配入如下自定义值进 state 里：

```json
"companies": [
      { company: '测试公司1', id: 1, createTime: +new Date() },
      { company: '测试公司2', id: 2, createTime: +new Date() },
      { company: '测试公司3', id: 3, createTime: +new Date() },
    ]
```

定义动态数据以后，我们需要绑定它到组件的属性中，我们找到相关属性的配置：

![image.png](https://img.alicdn.com/imgextra/i3/O1CN013Cu5OE1CXGRhyEmbJ_!!6000000000090-2-tps-3546-1792.png)

![image.png](https://img.alicdn.com/imgextra/i3/O1CN01iaK15j1bgIeO65svI_!!6000000003494-2-tps-3428-1640.png)

如图，输入表达式：

```javascript
this.state.companies
```

再结合上一节的“配置组件”操作，我们已经可以把表格的主体配置出来了：

![image.png](https://img.alicdn.com/imgextra/i2/O1CN01p8QJ5C1buxKDTS1cU_!!6000000003526-2-tps-3058-1640.png)

### 动态请求

我们进入代码区块，使用生命周期方法来完成动态数据的请求。假设提供数据的接口是：[http://rap2api.taobao.org/app/mock/250089/testCompanies](http://rap2api.taobao.org/app/mock/250089/testCompanies)，那么，我们可以在源码面板进行如下配置：

```typescript
class LowcodeComponent extends Component {
  state = {
    "text": "outer",
    "isShowDialog": false,
    "loading": false,
    "companies": [
      { company: '测试公司 1', id: 1, createTime: +new Date() },
      { company: '测试公司 2', id: 2, createTime: +new Date() },
      { company: '测试公司 3', id: 3, createTime: +new Date() },
    ]
  }
  componentDidMount() {
    this.setState({ loading: true })
    window.fetch('http://rap2api.taobao.org/app/mock/250089/testCompanies')
      .then((res) => res.json())
      .then((companies) => {
        this.setState({
          companies,
        })
      })
      .catch(err => console.error(err))
      .then(() => {
        this.setState({ loading: false })
      })
  }
}
```

在 `componentDidMount` 生命周期，将请求接口并设置 loading 和数据字段。

点击保存或叉关闭源码面板后，我们可以看到代码已经生效了：

![image.png](https://img.alicdn.com/imgextra/i3/O1CN01lqjW8e1f39G8Zm7hQ_!!6000000003950-2-tps-3058-1634.png)

### 配置插槽

我们可以用绑定数据的方法把 loading 绑在加载指示上：

![image.png](https://img.alicdn.com/imgextra/i1/O1CN01K3Pwjo1PKWQcoBl5K_!!6000000001822-2-tps-3170-1904.png)

![Feb-16-2022 20-24-35.gif](https://img.alicdn.com/imgextra/i2/O1CN01VGlZPS1JitoljrFFY_!!6000000001063-1-tps-1532-792.gif)

将 Loading 的“是否显示”字段绑定 `this.state.loading` 后，我们可以看到，这里暴露了一个插槽。插槽是可以任意扩展的预设部分，我们可以把其他的部分拖进插槽：

![Feb-16-2022 20-27-03.gif](https://img.alicdn.com/imgextra/i2/O1CN01HSBncU1XWRfPdwlPK_!!6000000002931-1-tps-1528-792.gif)

点击右上角的预览，我们能够看到完整的动态请求效果了： ![Feb-16-2022 20-28-36.gif](https://img.alicdn.com/imgextra/i3/O1CN01o5THZf1fkesw2nZEC_!!6000000004045-1-tps-1534-792.gif)

### 列挂钩浮层

为了能够让表格里的操作挂钩浮层，我们先拖入一个浮层： ![Feb-16-2022 20-32-09.gif](https://img.alicdn.com/imgextra/i2/O1CN01bX3SHk21Z8T4O6knp_!!6000000006998-1-tps-1532-792.gif)

使用大纲树能够临时显示和隐藏此浮层： ![Feb-16-2022 20-32-39.gif](https://img.alicdn.com/imgextra/i3/O1CN01ZtSp0P1LvNqYPeUHg_!!6000000001361-1-tps-1530-792.gif)

我们给表格增加一个数据列： ![Feb-16-2022 20-39-41.gif](https://img.alicdn.com/imgextra/i2/O1CN012K6qWI1hgCG6KwRF7_!!6000000004306-1-tps-1532-792.gif)

然后配置它的行为为“弹窗”： ![Feb-16-2022 20-40-05.gif](https://img.alicdn.com/imgextra/i2/O1CN016axZh61uc9ln0L3Rz_!!6000000006057-1-tps-1532-792.gif)

实现的效果如下： ![Feb-16-2022 20-42-51.gif](https://img.alicdn.com/imgextra/i4/O1CN018iana91j4l71QTmpE_!!6000000004495-1-tps-1534-792.gif)

### 事件回调

上述功能点中，我们是把操作行为绑定在数据列上的，这一节我们绑定到操作列中。在操作列按钮处，点击下方的“添加一项”： ![Feb-23-2022 11-58-02.gif](https://img.alicdn.com/imgextra/i4/O1CN01DsBoHQ1tyli2rtoFR_!!6000000005971-1-tps-1534-790.gif)

点击左侧的详情按钮，配置它的事件回调： ![Feb-23-2022 12-00-18.gif](https://img.alicdn.com/imgextra/i2/O1CN017BuNLP1LPmW8zH7hx_!!6000000001292-1-tps-1534-790.gif)

代码侧，我们配置这个回调函数：

```javascript
onClick_new(e, { rowKey, rowIndex, rowRecord }){
  window.Next.Message.show(JSON.stringify({ rowKey, rowIndex, rowRecord }))
}
```

保存。预览时我们可以看到效果了： ![Feb-23-2022 12-05-25.gif](https://img.alicdn.com/imgextra/i3/O1CN01CXi1zJ1N302paKUre_!!6000000001513-1-tps-1532-790.gif)

## 研究本例的 schema

我们把本例的 schema 保存在云端，您可以自行下载研究：[https://mo.m.taobao.com/marquex/lowcode-showcase-table](https://mo.m.taobao.com/marquex/lowcode-showcase-table)

您可以通过左下角的 Schema 面板直接导入本例子的 Schema。 ![image.png](https://img.alicdn.com/imgextra/i1/O1CN01z2LXgW1iFSklNRzTN_!!6000000004383-2-tps-3054-1620.png)

# 3. 如何通过按钮展示/隐藏弹窗

## 1.拖拽一个按钮

![image.png](https://img.alicdn.com/imgextra/i1/O1CN01kLaWA31D6WwTui9VW_!!6000000000167-2-tps-3584-1812.png)

## 2.拖拽一个弹窗

![image.png](https://img.alicdn.com/imgextra/i2/O1CN01rfRzLa1quEwUyulPc_!!6000000005555-2-tps-3578-1622.png)

## 3.查看弹窗 refId

![image.png](https://img.alicdn.com/imgextra/i1/O1CN01rEgPnW1cSqdWpG0YE_!!6000000003600-2-tps-3574-1588.png)

* 点击弹窗
* 点击右侧面板中的高级
* 找到 refId

![image.png](https://img.alicdn.com/imgextra/i3/O1CN01MXMfqn1rj4uKzlOh2_!!6000000005666-2-tps-3584-1796.png)

这里我们的 refId 是 "pro-dialog-entryl32xgrus"

## 4.隐藏弹窗

点击工具栏的隐藏小图标，将弹窗在画布中隐藏 ![image.png](https://img.alicdn.com/imgextra/i3/O1CN017Kamt71HFvWkpeK8j_!!6000000000729-2-tps-3578-1568.png)

## 5.按钮绑定事件

![image.png](https://img.alicdn.com/imgextra/i4/O1CN01SwJ0xx1u3LfX2h8yt_!!6000000005981-2-tps-3584-1814.png)

**通过下面的代码即可打开弹窗**

```typescript
this.$('pro-dialog-entryl32xgrus').open();
```
# 4. 设置器介绍

## 展示区域

设置器，又称为 Setter，主要展示在编辑器的右边区域，如下图： ![image.png](https://img.alicdn.com/imgextra/i4/O1CN01jN0toi1OknXWrPuYt_!!6000000001744-2-tps-3836-1730.png) 其中包含 属性、样式、事件、高级

* 属性：展示该物料常规的属性
* 样式：展示该物料样式的属性
* 事件：如果该物料有声明事件，则会出现事件面板，用于绑定事件。
* 高级：两个逻辑相关的属性，**条件渲染**和**循环**

## 设置器

上述区域中是有多项设置器的，对于一个组件来说，每一项配置都对应一个设置器，比如我们的配置是一个文本，我们需要的是文本设置器，我们需要配置的是数字，我们需要的就是数字设置器。 下图中的标题和按钮类型配置就分别是文本设置器和下拉框设置器。 ![image.png](https://img.alicdn.com/imgextra/i4/O1CN01Bl2hgm1GiUcXD3TOO_!!6000000000656-2-tps-2120-1460.png)

我们提供了常用的设置器作为内置设置器，也提供了定制能力帮助大家开发特定需求的设置器。
# 5. 源码面板详解

在源码面板中，您可以完成低代码中的代码部分编写。

## 面板功能拆解

![image.png](https://img.alicdn.com/imgextra/i4/O1CN01pRxmmD1agTBVwCO5x_!!6000000003359-2-tps-2502-1740.png)

### 代码编辑面板

代码编辑面板允许您书写 JavaScript 代码，并支持 JSX 语法。 由于依赖了 Babel，所以书写的 JSX 和 Chrome 80+ 以后的新语法也会被自动编译：

| 编译前                                                                                                   | 编译后                                                                                                    |
| ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| ![image.png](https://img.alicdn.com/imgextra/i4/O1CN01xI9RVX1yV46HbW02H_!!6000000006583-2-tps-670-190.png) | ![image.png](https://img.alicdn.com/imgextra/i1/O1CN012exYQL1y37wKM7VFT_!!6000000006522-2-tps-2094-110.png) |
| ![image.png](https://img.alicdn.com/imgextra/i4/O1CN01pK2rPi1lhLij4m3o7_!!6000000004850-2-tps-434-120.png) | ![image.png](https://img.alicdn.com/imgextra/i2/O1CN01ti4n9m1ihOupktQow_!!6000000004444-2-tps-2536-120.png) |

> 注：因为编译结果会被 `@babel/runtime` 干扰，目前面板不支持 `async await`或 `{ ...arr }` 形态的语法编译。如果您需要此类编译，您可以考虑在读取 schema 中的 `originCode` 之后自己手动通过 babel 编译。

#### 全局变量引用

在代码中，您可以通过 window 来引用全局变量。资产包中的 packages 都是通过 UMD 方式引入的对应内容，如果您引入了 Fusion Next（Demo 中默认引入），那么可以通过此方法直接唤起 Fusion Next 的内容，如弹窗提示：

```typescript
window.Next.Message.success('成功')
```

![image.png](https://img.alicdn.com/imgextra/i1/O1CN01Fxjd801p4eigEBpb6_!!6000000005307-2-tps-238-114.png)

#### 局部变量引用

您可以在成员函数中访问到如下变量：

* `this.state`
* `this.setState`
* `this.context.appHelper.utils`
* `this.context.appHelper.constants`
* `this.context.appHelper.requestHandlerMap`
* `this.context.components`

#### 读、写与异常处理

* 读取：每次打开面板时，都会尝试读取 schema 中的 originCode 字段，如果没有，则从 schema 上的字段还原代码；
* 写入：在关闭代码编辑面板（主动点击叉或者点击非代码编辑区块的被动关闭都算）时，将自动写入到 schema 中；您也可以在编辑过程中点击“保存”按钮手动保存；

| 源码面板中                                                                                                                   | Schema 中                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| 本地数据初始值设置：![image.png](https://img.alicdn.com/imgextra/i4/O1CN01V6iaTY1gVNHi7gQfK_!!6000000004147-2-tps-370-146.png) | ![image.png](https://img.alicdn.com/imgextra/i2/O1CN010rhIPa268BEfGmzO6_!!6000000007616-2-tps-2098-826.png) |
| 生命周期方法：![image.png](https://img.alicdn.com/imgextra/i4/O1CN010Y1TxV1QOvrVLRUjD_!!6000000001967-2-tps-478-260.png)       | ![image.png](https://img.alicdn.com/imgextra/i3/O1CN01pbJzVQ1VSfAL7Lh8G_!!6000000002652-2-tps-2010-836.png) |
| 自定义函数：![image.png](https://img.alicdn.com/imgextra/i4/O1CN01S2gjFk1CU3fm61eiD_!!6000000000083-2-tps-660-642.png)         | ![image.png](https://img.alicdn.com/imgextra/i2/O1CN01X35YxU1GUkjj1YWVj_!!6000000000626-2-tps-1862-822.png) |
| 编译前全量代码：![image.png](https://img.alicdn.com/imgextra/i2/O1CN01sbiK9N1kc1Uxp1OHY_!!6000000004703-2-tps-762-1122.png)    | ![image.png](https://img.alicdn.com/imgextra/i3/O1CN01adKSg61QXAzRjQ4bm_!!6000000001985-2-tps-1906-796.png) |

* 异常处理：如果代码解析失败，它将无法被正常保存到 schema 中，此时编辑器会弹层提示：

![image.png](https://img.alicdn.com/imgextra/i4/O1CN01aSzh8o26rWRu6zXFE_!!6000000007715-2-tps-3068-1638.png)

### 样式编辑面板

您可以在这里书写 CSS 内容。它对应 schema 中的 css 字段：

| 源码面板中                                                                                               | Schema 中                                                                                                 |
| ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| ![image.png](https://img.alicdn.com/imgextra/i2/O1CN01cuWt4L27fRcW5WIP9_!!6000000007824-2-tps-634-388.png) | ![image.png](https://img.alicdn.com/imgextra/i4/O1CN01Edu7Gy1MzKsb2iss8_!!6000000001505-2-tps-1646-582.png) |

## 对接代码

### 生命周期对接

如果您书写了视图相关的声明周期方法，那么对应的方法会在视图的特定周期被调用。支持的生命周期函数在《阿里巴巴中后台前端搭建协议规范》中被定义，包含：

```typescript
{
  componentDidMount(): void;
  constructor(props: Record<string, any>, context: any);
  render(): void;
  componentDidUpdate(prevProps: Record<string, any>, prevState: Record<string, any>, snapshot: Record<string, any>): void;
  componentWillUnmount(): void;
  componentDidCatch(error: Error, info: any): void;
}
```

### 设置器面板对接

书写完了函数 / state 后，您可以在右侧的设置器面板中配置对代码的部分。

通常书写代码是为了对接低代码配置中的“变量绑定”、“事件回调”、“条件判断”和“循环”部分的。

#### 变量绑定

![image.png](https://img.alicdn.com/imgextra/i2/O1CN01wcgwOI1wOXDtgfrgD_!!6000000006298-2-tps-2738-1464.png)![image.png](https://img.alicdn.com/imgextra/i4/O1CN01GYVAw41FlrvEyFcCO_!!6000000000528-2-tps-1528-1166.png)

```json
{
  "componentName": "NextBlockCell",
  "id": "node_ockzmje8tf5",
  "props": {
    "bodyPadding": {
      "type": "JSExpression",
      "value": "this.state.text",
      "mock": ""
    }
  }
}
```

#### 事件回调

![image.png](https://img.alicdn.com/imgextra/i1/O1CN01B0tvgw1O6x58dbbIb_!!6000000001657-2-tps-2734-1452.png)![image.png](https://img.alicdn.com/imgextra/i1/O1CN01sD9g2n1tQQ0OjQkcY_!!6000000005896-2-tps-1670-1162.png)

```json
{
  "componentName": "Filter",
  "id": "node_ockzmj0cl11w",
  "props": {
    "__events": {
      "eventDataList": [
        {
          "type": "componentEvent",
          "name": "onSearch",
          "relatedEventName": "closeDialog"
        }
      ]
    },
    "onSearch": {
      "type": "JSFunction",
      "value": "function(){this.onSearch.apply(this,Array.prototype.slice.call(arguments).concat([])) }"
    }
  }
}
```

#### 条件判断

![image.png](https://img.alicdn.com/imgextra/i2/O1CN01zXqec823EBaCutOY2_!!6000000007223-2-tps-2738-1452.png)![image.png](https://img.alicdn.com/imgextra/i2/O1CN01Ze3snL24BGfuRIMCl_!!6000000007352-2-tps-1528-1166.png)

```json
{
  "componentName": "Filter",
  "id": "node_ockzmj0cl11w",
  "condition": {
    "type": "JSExpression",
    "value": "this.state.text",
    "mock": true
  }
}
```

#### 循环

![image.png](https://img.alicdn.com/imgextra/i2/O1CN01Kbj6XP297fe0BvhKz_!!6000000008021-2-tps-2746-1460.png)![image.png](https://img.alicdn.com/imgextra/i1/O1CN018Ogesd1qnN0IOKRDZ_!!6000000005540-2-tps-1528-1166.png)

```json
{
  "componentName": "Filter",
  "id": "node_ockzmj0cl11w",
  "loop": {
    "type": "JSExpression",
    "value": "this.state.text",
    "mock": true
  }
}
```
# 6. 数据源面板详解

## 🪚 概述

数据源面板主要负责管理低代码中远程数据源内容，通过可视化编辑的方式操作低代码协议中的数据源 Schema，配合 [数据源引擎](https://lowcode-engine.cn/site/docs/guide/design/datasourceEngine) 即可实现低代码中数据源的生产和消费；

![image.png](https://img.alicdn.com/imgextra/i1/O1CN0170HeBg276B7fM9rqh_!!6000000007747-2-tps-2878-1642.png)

数据源面板

## ❓如何使用

> 面板内包含了数据源创建、删除、编辑、排序、导入导出、复制以及搜索等能力，内置支持了 `fecth` & `JSONP`两种常用远程请求类型；

### 三步创建一个数据源

![image.png](https://img.alicdn.com/imgextra/i2/O1CN01bkgbqj1cOGfwQtEif_!!6000000003590-2-tps-2878-1638.png)

三步创建数据源
# 7. demo 使用相关 API

## 数据源相关

### 请求数据源

```javascript
// 请求 userList（userList 在数据源面板中定义）

this.dataSourceMap['userList'].load({
    data: {}
}).then(res => {})
  .catch(error => {});
```

### 获取数据源的值

```javascript
const { userList } = this.state;
```

### 手动修改数据源值

```javascript
// 获取数据源面板中定义的值
const { user } = this.state;

// 修改 state 值
this.setState({
    user: {}
});
```

# 以下为编码注意点

### 1. 向后端发送请求我用的是fetch函数
fetch函数模版
```javascript
async onSearchById(value) {
    var url = "";
    console.log(value.getById)
    if (value.getById) {
        url = 'http://localhost:5050/Test/GetByIdController/id' + '?id=' + value.getById;
    } else {
        url = 'http://localhost:5050/test/getcontroller';
    }
    const { info } = this.state;
    const response = await fetch(url, {
        method: 'POST', //GET, POST, PUT, DELETE, etc.
        mode: 'cors',// no-cors, *cors, same-origin 
        cache: 'no-cache',// default, no-cache, reload, force-cache, only-if-cached
        credentials: 'same-origin',// include, *same-origin, omit
        headers: {
            'Content-Type': 'application/json'
            // 'Content-Type': 'application/x-www-form-urlencoded',
        },
        redirect: 'follow',// manual, *follow, error
        referrerPolicy: 'no-referrer',// noreferrer, *no-refrrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin,
        //请求体
        body: JSON.stringify({
            id: value.getById
        })
    });
    response.json().then((data) => {
        console.log(data);
        if (data) {
            this.setState({
                info: data.data
            })
            Next.Notification.success({
                title: "成功",
                style: {
                    width: 600,
                    marginLeft: -255
                }
            });
        }
        else {
            Next.Notification.error({
                title: "失败",
                style: {
                    width: 600,
                    marginLeft: -255
                }
            })
        }
    })

}

```

### 2. 响应数据的处理
对于高级表格的数据源必须是数组形式的，每个数组元素对应表格中的一行。在表格中所遍历的数组元素中的字段必须为基本数据类型，不可为数组等其他类型。这里我将响应的数据进行了提取操作，JavaScript不支持内部类，我用的JavaScript中的函数进行保存的（也可以在LowcodeComponent类外面再声明一个类进行映射操作）。
```javascript
  Robot(uuid, ip, current_map, current_group, dispatchable, current_order_id, current_order_state, battery_level, confidence, locked, reloc_status, procBusiness) {
    return {
      "uuid": uuid,
      "ip": ip,
      "current_map": current_map,
      "current_group": current_group,
      "dispatchable":dispatchable,
      "current_order_id": current_order_id,
      "current_order_state": current_order_state,
      "battery_level": battery_level,
      "confidence": confidence,
      "locked": locked,
      "reloc_status": reloc_status,
      "procBusiness": procBusiness
    };
```

### 3. 启动阿里低代码平台报错 error in ./node_modules/@alifd/next/es/grid/main.scss
![image.png](./img/error_node_module.png)
错误提示是在main.scss这个文件里有一行代码错误了。
所以直接找到这个文件对应的这行，然后把这行删掉
```javascript
@media #{$query} { @content; }
```

### 4. 报错“NextP component is not found in components list!”
高级对话框和高级表单联用会报错
解决方案：手动编辑schema，删除红框处的“段落”可修复
![image.png](./img/删除段落.png)

### 5. 前端项目的打包发布
点击出码按钮后会得到一个压缩包，对其进行解压并切换到该目录后，执行命令`npm run build`将会直接进行打包。
命令:
>npm run build

作用：用vue-cli内部集成的webpack，把 .vue, .less, .js 等打包成浏览器可直接执行的代码 html，css，js。

结果：会在项目根目录下创建 /build目录，在这目录下产出打包后的结果。

### 6. build项目之后打开index.html页面没有内容显示
编辑index.html源码,在引用css与js的地方删除第一个斜杠
![image.png](./img/error_html.png)
