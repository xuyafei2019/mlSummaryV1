
@[toc]
# YFX ML Algorithm Summary---33
## 01 Logistic Regression
1，logistic function or sigmoid function
$s(t)=\dfrac{1}{1+e^{-t}}$
$Pr(y_i=1|x_i)=s(x_i\beta)$
$Pr(y_i=0|x_i)=1-s(x_i\beta)$

likelihood function---:
$L(\beta;y_i,x_i)=[s(x_i\beta)]^{y_i}[1-s(x_i\beta)]^{1-y_i}$

$L(\beta;Y,X)=\Pi_{i=1}^N[s(x_i\beta)]^{y_i}[1-s(x_i\beta)]^{1-y_i}$

log-likelihood function:
$l(\beta;Y,X)=\Sigma_{i=1}^N[-ln(1+e^{x_i\beta})+y_ix_i\beta]$

MLE:
$\hat{\beta}=\mathop{\arg\max}_{\beta}l(\beta;Y,X)$
$\frac{\partial l}{\partial \beta}=\frac{\partial \{\Sigma_{i=1}^N[-ln(1+e^{x_i\beta})+y_ix_i\beta]\}}{\partial \beta}=\Sigma_{i=1}^N[-\frac{x_ie^{x_i\beta}}{1+e^{x_i\beta}}+y_ix_i]=\Sigma_{i=1}^N[y_i-s(x_i\beta)]x_i=0$

that is
$\Sigma_{i=1}^N[y_i-s(x_i\beta)]x_i=0$

since there is no analytical solution, hence using numerical method to solve this problem, e.g. Newton-Raphson-Method,
$\hat{\beta}_t=\hat{\beta}_{t-1}+\delta{\underbrace{[\frac{\partial^2 l(\hat{\beta}_{t-1};Y,X)}{\partial \beta \partial \beta^T}]}_{Hessian}}^{-1}\underbrace{\frac{\partial l(\hat{\beta}_{t-1};Y,X)}{\partial \beta}}_{Score}$


## 02 SVD Decompostion
1, $A_{m\times n}=U\Sigma V^\top$, $U_{m\times m}, \Sigma_{m\times n}, V_{n\times n}$
2, $\Sigma$‘s对角线上的值diagnal value is called sigular value奇异值
3, $U^TU=I, V^TV=I​$’
4, $(A^TA)_{n\times n}$'s eigenvectors composes $V_{n\times n}$

## 03 boosting, bagging, stacking集成算法
1. 常见术语base learner，multiclassifiers，
2. error常见来源：noise, bias and variance.
3. Combinations of multiple classifiers decrease variance
4. bagging和boosting都需要抽取样本，bagging（abbr. of bootstrap aggregating）采用bootstrap抽取样本，即有放回抽样，那么每个observation都有相同的概率被抽出来。而boosting不同之处在于，每个点被抽出来的概率不同，采用weighted sampling。
5. ​

| 项目                | bagging                                  | boosting                                 |
| :---------------- | :--------------------------------------- | :--------------------------------------- |
| 样本抽样方式            | 所有样本点sample with same probability        | sampling with weighted probability       |
| training stage    | parallel, i.e. each model is trained independently | sequential                               |
| 样本调整              | 不调整                                      | 被错分的样本点需要重新调整weight，增加weight             |
| 分类问题              | 把$N$个模型的分类结果通过majority vote得出结果          | 把$N$个模型的分类结果通过weighted形式给出，预测或分类能力强的模型会被分配更大的weight。单模型的训练中boosting需要追踪每个模型的error。例如在adaboost中，error不能小于50%才会被保留下来 |
| bias and variance | 不能改变bias，可以降低variance                    | 可以降低variance同时降低bias                     |
| overfitting       | bagging可以避免overfit                       | boosting不能避免overfit而可能增加overfit          |
7. boosting和bagging很大的两个不同点在于两个加权weighted
- 第一，样本需要加权，被错分的样本点有更大的被抽出的概率
- 第二，模型组合需要加权，表现更好的模型在预测和分类时权重更大
8. bagging和boosting的几个图

| stage        | single，bagging，boosting                  |
| :----------- | :--------------------------------------- |
| model pool   | ![Single Bagging and Boosting 1 learner N learners From 1 to N Algorithm Comparison Versus](https://quantdare.com/wp-content/uploads/2016/04/bb1-800x221.png) |
| sampling     | ![Single Bagging and Boosting Training set Multiple sets Random sampling with replacement Over weighted data Algorithm Comparison Versus](https://quantdare.com/wp-content/uploads/2016/04/bb2-800x307.png) |
| training     | ![Single Bagging and Boosting Parallel Sequential Algorithm Comparison Versus](https://quantdare.com/wp-content/uploads/2016/04/bb3-800x307.png) |
| predict      | ![Single Bagging and Boosting Single estimate Simple average Weighted average Algorithm Comparison Versus](https://quantdare.com/wp-content/uploads/2016/04/bb4-800x307.png) |
| single model | ![Single Bagging and Boosting Training stage Train and keep Train and evaluate Update sample weights Update learners weights Algorithm Comparison Versus](https://quantdare.com/wp-content/uploads/2016/04/bb5-800x285.png) |
    8. 二者详细总结

| 项目                | 相同点                                 | 不同点                                      |
| :---------------- | :---------------------------------- | :--------------------------------------- |
| 模型组合              | 都是把$N$个模型组合成一个模型                    | bg中每个模型都是独立的模型，bst中顺序建模，只要前一个模型存在分类错误就添加新模型 |
| 样本                | 有放回抽样                               | bg所有点被抽中的概率相同,bst被错分的点权重增加               |
| 模型预测结果            | 求平均或多数投票原则                          | bg简单平均，bst加权平均，能力强的模型权重大                 |
| variance and bias | 都reduce variance，increase stability | bg减小overfit，bst增大overfit；bst减小bias，bg不能  |




## 04 AdaBoost, LPBoost, XGBoost, GradientBoost, BrownBoost.


- ​

# 欢迎使用Markdown编辑器写博客

本Markdown编辑器使用[StackEdit][6]修改而来，用它写博客，将会带来全新的体验哦：

- **Markdown和扩展Markdown简洁的语法**
- **代码块高亮**
- **图片链接和图片上传**
- ***LaTex*数学公式**
- **UML序列图和流程图**
- **离线写博客**
- **导入导出Markdown文件**
- **丰富的快捷键**

-------------------

## 快捷键

 - 加粗    `Ctrl + B` 
 - 斜体    `Ctrl + I` 
 - 引用    `Ctrl + Q`
 - 插入链接    `Ctrl + L`
 - 插入代码    `Ctrl + K`
 - 插入图片    `Ctrl + G`
 - 提升标题    `Ctrl + H`
 - 有序列表    `Ctrl + O`
 - 无序列表    `Ctrl + U`
 - 横线    `Ctrl + R`
 - 撤销    `Ctrl + Z`
 - 重做    `Ctrl + Y`

## Markdown及扩展

> Markdown 是一种轻量级标记语言，它允许人们使用易读易写的纯文本格式编写文档，然后转换成格式丰富的HTML页面。    —— <a href="https://zh.wikipedia.org/wiki/Markdown" target="_blank"> [ 维基百科 ]

使用简单的符号标识不同的标题，将某些文字标记为**粗体**或者*斜体*，创建一个[链接](http://www.csdn.net)等，详细语法参考帮助？。

本编辑器支持 **Markdown Extra** , 　扩展了很多好用的功能。具体请参考[Github][2].  

### 表格

**Markdown　Extra**　表格语法：

| 项目       | 价格    |
| -------- | ----- |
| Computer | $1600 |
| Phone    | $12   |
| Pipe     | $1    |

可以使用冒号来定义对齐方式：

| 项目       |     价格 |  数量  |
| :------- | -----: | :--: |
| Computer | 1600 元 |  5   |
| Phone    |   12 元 |  12  |
| Pipe     |    1 元 | 234  |

###定义列表

**Markdown　Extra**　定义列表语法：
项目１
项目２
:   定义 A
:   定义 B

项目３
:   定义 C

:   定义 D

	> 定义D内容

### 代码块
代码块语法遵循标准markdown代码，例如：
```python
@[toc]requires_authorization
def somefunc(param1='', param2=0):
    '''A docstring'''
    if param1 > param2: # interesting
        print 'Greater'
    return (param2 - param1 + 1) or None
class SomeClass:
    pass
>>> message = '''interpreter
... prompt'''
```

###脚注
生成一个脚注[^footnote].
[^footnote]: 这里是 **脚注** 的 *内容*.

### 目录
用 `[TOC]`来生成目录：

@[toc]
### 数学公式
使用MathJax渲染*LaTex* 数学公式，详见[math.stackexchange.com][1].

 - 行内公式，数学公式为：$\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$。
 - 块级公式：

  $$x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} $$

更多LaTex语法请参考 [这儿][3].

对于$$a^2+b^2=c^2 \tag {1.2}$$由公式$(1.2)$即可得到结论。

### UML 图:

可以渲染序列图：

```mermaid
sequenceDiagram
张三->>李四: 嘿，小四儿, 写博客了没?
Note right of 李四: 李四愣了一下，说：
李四-->>张三: 忙得吐血，哪有时间写。
```

或者流程图：

```mermaid
flowchat
st=>start: 开始
e=>end: 结束
op=>operation: 我的操作
cond=>condition: 确认？

st->op->cond
cond(yes)->e
cond(no)->op
```

- 关于 **序列图** 语法，参考 [这儿][4],
- 关于 **流程图** 语法，参考 [这儿][5].

## 离线写博客

即使用户在没有网络的情况下，也可以通过本编辑器离线写博客（直接在曾经使用过的浏览器中输入[write.blog.csdn.net/mdeditor](http://write.blog.csdn.net/mdeditor)即可。**Markdown编辑器**使用浏览器离线存储将内容保存在本地。

用户写博客的过程中，内容实时保存在浏览器缓存中，在用户关闭浏览器或者其它异常情况下，内容不会丢失。用户再次打开浏览器时，会显示上次用户正在编辑的没有发表的内容。

博客发表后，本地缓存将被删除。　

用户可以选择 <i class="icon-disk"></i> 把正在写的博客保存到服务器草稿箱，即使换浏览器或者清除缓存，内容也不会丢失。

> **注意：**虽然浏览器存储大部分时候都比较可靠，但为了您的数据安全，在联网后，**请务必及时发表或者保存到服务器草稿箱**。

##浏览器兼容

    1. 目前，本编辑器对Chrome浏览器支持最为完整。建议大家使用较新版本的Chrome。
    2. IE９以下不支持
    3. IE９，１０，１１存在以下问题
    1. 不支持离线功能
    2. IE9不支持文件导入导出
    3. IE10不支持拖拽文件导入

---------

[1]: http://math.stackexchange.com/
[2]: https://github.com/jmcmanus/pagedown-extra "Pagedown Extra"
[3]: http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
[4]: http://bramp.github.io/js-sequence-diagrams/
[5]: http://adrai.github.io/flowchart.js/
[6]: https://github.com/benweet/s


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5ODY5OTU0MzIsMjA3MjkyODE1MF19
-->