

# <b>全自动菌柄农场 骨粉效率版本v5.1</b>

公式无法正确显示，推荐使用Typora 获得更好观看体验。

配合视频[全自动菌柄树场]()观感更佳。

[TOC]



## <b>时间线</b>

- 20w12a发布  <b>2020/03/18</b>

> 菌类、菌索和下界苗
>
> - 对菌岩使用骨粉时会在其上生长。

- [Minecraft 20w12a Snapshot Review by Rays Works](https://www.bilibili.com/video/BV1eE411A75Z?p=2) 提出全自动树场概念 <b>2020/03/18</b>
- [20w12a 绯红菌/诡异菌树场 by Sela_Col](https://www.bilibili.com/video/BV1rE411P7eg) 感应式 <b>2020/03/20</b>
- 全自动巨型菌类树场 [BV13E411P7YT](https://www.bilibili.com/video/BV13E411P7YT) ，我的首个全自动树场发布 <b>2020/03/21</b>
- 全自动菌柄树场 生存友好版 新增自动切换模式[BV1nE411c7k5](https://www.bilibili.com/video/BV1nE411c7k5) 我的第二个树场<b>2020/03/23</b>
- [自动菌类农场 可切换模式 by ilmango](https://www.bilibili.com/video/BV1uA411h7Cj) 推地板刷菌类 <b>2020/03/24</b>
- 设计完成核心部件到第一个原型机完成 <b>2020/04/04</b>
- 20w15a发布 <b>2020/04/08</b>

> 菌类、下界苗、菌索、缠怨藤、下界疣、下界疣块、诡异疣块和垂泪藤
> 现在可用于堆肥。

- [Minecraft News: 20w15a Blackstone by ilmango](https://www.bilibili.com/video/BV1iz411b7JT) 提出可自我循环利用的全自动树场概念 <b>2020/04/08</b>
- [200粉丝纪念 最快全自动菌柄树场 35k 菌柄/小时](https://www.bilibili.com/video/BV12K411L7sH) 我的效率为优先设计的全自动树场 <b>2020/04/09</b>

## <b>树场介绍</b>

### <b>树场特点</b>

- 检测式效率优先的全自动菌柄树场
- 高稳定性、与方向无关、与位置无关、可镜像
- 菌岩自修复
- 工作频率可调节
- 宽度高度可定制
- 基于潜影盒的物流
- 统一输入输出



### <b>树场组成</b>

- <b>推出面积为5*7的树场 4gt</b>

  树场由1个贴着菌岩的<b>主发射器di<sub>1</sub></b>用来催熟绯红/诡异菌岩来获得对应的菌类（树种）。

  催熟菌岩产生杂草的范围为5*5，因此为了效率最小的树场就是5格宽。

  还有四个紧贴着菌岩的<b>辅发射器di<sub>2</sub></b>用来修复小概率发生的菌岩退化成下界岩的事件。

  除此之外还有5个在菌岩上一格的<b>发射器组di<sub>3</sub></b>用来催熟菌类。

  底部向上推出菌柄或者疣块的<b>粘性活塞组p<sub>1</sub></b>，菌柄或者疣块的在菌岩表面会阻止新的菌类生成。

  横向来回推动的<b>活塞对p<sub>2</sub></b>，用于刷新菌柄的生成。

  用于检测菌柄生长情况的<b>投掷器dr<sub>1</sub></b>。

  用于更新bud状态<b>dr<sub>1</sub></b>和<b>p<sub>1</sub></b>的<b>活塞组p<sub>3</sub></b>
  
- <b>推出面积为10\*24\*2 4gt</b>

  设计之初就考虑到堆叠的问题，这种设计可以很方便的通过横向堆叠，堆叠到12宽，不过考虑到骨粉效率，已经TNT的爆炸范围，将宽度定为了10宽。高度可以自定义，由于巨型菌类最高只能生长24格，因此最大高度也到此为止了。

- <b>推出面积为10\*24\*2 8gt</b>

  只通过降低<b>p<sub>2</sub></b>的工作频率，来提升骨粉效率，不过相应的整体效率会下降。具体可以参考[附录](#附录)。



注意： <b>活塞对p<sub>2</sub></b>的单独一个活塞的周期为8gt，但是算上来回推动，这里为了方便表述，定义<b>活塞对p<sub>2</sub></b>的周期为4gt。



大部分时钟都工作在4gt,因此我定义一个特定的信号为“<b>0011</b>”的4gt信号周期为一个<b>工作周期T</b>。意义在于，如果在本周期事件没有完成，会顺延到下一工作周期。具体来说，不会因为<b>p<sub>1</sub></b>菌岩上推阻止<b>p<sub>2</sub></b>活塞的横向移动而改变<b>p<sub>2</sub></b>时序，因为活塞的运作时<b>被动</b>的。



### <b>运作方式</b>

每当生成菌类被催熟长大，<b>p<sub>1</sub></b>由于bud尝试向上推出。无论<b>p<sub>1</sub></b>是否推出，都会在一个工作周期T结束后qc激活感应用的投掷器组,经过10gt的延时激活活塞墙。如果<b>p<sub>1</sub></b>没有推出，则会在向上推出后再次激活活塞墙。<b>p<sub>1</sub></b>也由于bud自动收回推出的菌岩。收回的菌岩会被提供bud信号源的侦测器充能，成为<b>di<sub>1</sub> di<sub>2</sub></b>的信号源，从而自动修复菌岩。

整个树场有4组独立的时钟用于控制。包括<b>di<sub>1</sub></b>的4gt时钟<b>c<sub>1</sub></b>；<b>p<sub>2</sub></b> 的4gt时钟<b>c<sub>2</sub></b>；<b>p<sub>3</sub>, p<sub>1</sub>, dr<sub>1</sub></b>的4gt时钟<b>c<sub>3</sub></b> 以及 <b>d<sub>2</sub></b>的长时钟<b>c<sub>4</sub></b>，都满足<b>工作周期T</b>。

这就涉及了怎么协同工作的问题，比如怎样在横向推出的时候能正确的收回菌岩,怎样在正确的时间催熟、修复菌岩。时钟的<b>相位</b>满足一下公式即可：
$$
\frac{1}{n}c_4=c_3=c_2-1=c_1,n\in N^+
$$
漏斗计时器物品数量<b>x</b>与其周期<b>C</b>的关系如下：
$$
\begin{equation}
C=\left\{
\begin{aligned}
&7&&{x=1}\\
&4(4x-3)&&{x>1,x\in N^+}\\
\end{aligned}
\right.
\end{equation}
$$
只要保证漏斗中的数量x>1，可以与4gt时钟保持同步。顺便说一句芒果牌的计时器不适用。

值得注意的是菌类的生成与催熟是在同1gt发生，这就要求在微时序上<b>di<sub>1</sub></b>要优先于<b>di<sub>3</sub></b>。

如果<b>p<sub>1</sub></b>向上推出，它与<b>p<sub>2</sub></b>横向推出也是在同1gt激活，微时序上<b>p<sub>1</sub></b>优先于<b>p<sub>2</sub></b>，收回同理。



#### <b>1gt的相位差</b>

通过研究发现，直接被拉杆或者红石线激活的活塞和同一信号源加了一个中继器激活的活塞，推出活塞臂的时间差为1gt，而不是2gt。而如果信号源先通过比较器中继器或者侦测器过滤一遍后，输出的信号相位差则为2gt。这和游戏运行的微时序有关，利用这个特性，可以轻松创造1gt相位差。

因此输入信号需要是玩家直接激活或者利用活塞推动红石块等方式。

注意： <b>p<sub>1</sub>p<sub>2</sub></b>活塞旁有其他的方块更新干扰会改变这一优先级。



### <b>骨粉来源</b>

首先是理念上面的问题，做这个树场的初衷就为了将树场推向<b>全自动</b>化。如果哪各环节还需要玩家过多的参与，我想也违背了这一点。这个农场的骨粉消耗量相当的惊人，<b>推出面积为10\*24\*2</b> 4gt模式下，有4个工作在4gt的<b>主发射器di<sub>1</sub></b>在同时催熟着菌岩，来尝试生成菌柄。平均下来每一gt都有骨粉在消耗，即使有回收的骨粉，消耗量仍然巨大，具体数据可以参照表格。如果直接输入骨粉的话系统的速度可能跟不上，因此我建立基于了潜影盒的物流系统。

同上的理念问题，如果骨粉还需要玩家手动获取，这也失去了<b>全自动</b>农场的意义。如果不是实时输入输出，也可先囤积一部分骨粉，待一定量后输入系统，快速收获数量可观的菌柄。



<b>推出面积为10\*24\*2的树场 4gt 绯红菌</b> 

此配置下有4个工作在周期为4gt的 <b>主发射器di<sub>1</sub></b>

基础骨粉消耗量：
$$
4*\frac{1}{4}/gt*20gt/s*3600s/h=72000/h
$$
|                                | 疣块  | 菌类、菌索 | 西瓜片、仙人掌 | 海带  | 鱼   | 骨头 |
| ------------------------------ | ----- | ---------- | -------------- | ----- | ---- | ---- |
| 生产1个骨粉平均值              | 8.24  | 10.77      | 14             | 23.33 | 20   | 0.33 |
| 基础骨粉消耗所需的产量 k/h     | 593.3 | 775.4      | 770            | 1283  | 1100 | 24   |
| 实测产量 k/h                   | 46    | 115        | -              | -     | -    | -    |

另外需要添加骨粉的速度：
$$
72000/h-(\frac{46000}{8.24h}+\frac{115000}{10.77h}) = 55740/h
$$
除了骨头提供骨粉的方式，其它都是几乎不可能实现的规模。除了可以手动合成骨粉提供骨粉以外，为了强行符合全自动的理念我决定使用carpet extra mod，并开启`autoCraftingDropper`。

通过实测摔落杀死1008只骷髅获得1025个骨头，如果要保证农场能持续运行，按照这种比例骷髅的处理的速度至少为18k/h。[Gnembon funfarm 15](https://www.youtube.com/watch?v=guvMmdeZqiI) 一个小自然刷怪农场就有8.3k/h骨头的效率，只需要稍微拓展一下就可以完美应付。

<b>堆肥桶</b>

|                            | 疣块 | 菌类/菌索 | 下界苗 |
| -------------------------- | ---- | --------- | ------ |
| 实测堆肥桶处理速度 k/h     | 7.7  | 8         | 8.1    |
| 需要新增堆肥桶的数量       | 6    | 15        | 0      |



其他模式的农场数据会[表格](#附录)中。



#### <b>自动合成</b>

Carpet extra mod 是gnembon对 Carpet mod的补充。作者本人也在介绍视频[av70188771](https://www.bilibili.com/video/av70188771/)中提到，Carpet添加的是他认为需要被添加并符合原版精神的内容，Carpet extra则是对原版较大改动，并认为仍想要被添加的功能。

我最希望被mojang官方加入的功能就有`autoCraftingDropper` 自动合成，`movableBlockEntities`可推动的方块实体。ilmango也多次宣传，比如[1.14~1.15空岛生存系列](https://www.bilibili.com/video/BV1z441147QC)，[How Movable Block Entities Could Enhance Your Game Experience](https://www.youtube.com/watch?v=1vML5LogGaE)。

 Gnembon单独出视频介绍过`autoCraftingDropper`，不过似乎没有搬运[Auto-Crafting Dropper](https://www.youtube.com/watch?v=bwnmFF6LYSo)。

这里稍微介绍一下。只要投掷器的面朝向工作台，通过其他投掷器或者漏斗输入的投掷器内部存储每一格都只能缓存一个物品，一一对应工作台的九宫格。每接受一次脉冲信号就完成一次合成，合成好的的物品会从工作台正中心以掉落物形式弹出,如果无法合成的合成表，会随机弹出一格物品。

因此物品的输入速度与投掷器接收到的脉冲的频率就共同决定了自动合成的速度。

视频中展示的是8个工作台的自动合成系统。它由我设计的两倍漏斗速度输入的合成模块，以1:3的数量比搭配gpw的双倍潜影盒装盒器组成。

因此输入速度为16倍漏斗速度为：144000 /h
$$
input\_speed=2*crafting\_table*hopper\_speed
$$


输出满盒骨粉的速度为：250 盒/h
$$
output\_speed=input\_speed*\frac{output\_num}{input\_num}*\frac{1}{stack\_num*shuker\_box\_slot\_num}
$$
实际需求时只需要<b>2</b>个工作台足够满足此树场的实时输入输出的骨粉需求。



### <b>TNT处理</b>

TNT组由3格独立的TNT模块组成，每个模块与其上方的模块相距8格。通过方块交换器，切换侦测器在2档、3档、4档中继器循环，发射信号长度分别是4gt、6gt、8gt来控制落点。因此每个TNT模块在一个周期中释放3个不同落点的TNT。一共包含9个不同高度的落点，用于处理24格高的菌柄与疣块。

#### <b>损失率</b>

如果观察[表格](#生产数据表格)，你会发现推出面积越大，单位面积的效率越低。单位面积效率低的来源除了树本身的生长特性以外，即生成高树的概率要低于矮树。还有另外一个重要的原因是，更高的位置的掉落物有更大的几率卡在底端的方块上，而没有被收集到。这也是我迟迟没有发布的原因之一，损失率不低。想过很多解决办法，但都没有在不影响效率的情况下，减少损失率，如果有什么好的办法欢迎讨论。



### <b>卡顿</b>

由于架构需求，不得不使用大量的高频。不过尽量减少红石粉的使用，增加遮光版、建造在低Y值的位置来减少光照更新，尽量少使用漏斗矿车与双排箱子，活塞推动的方块在同一区块等等方式来减少卡顿。

Carpet Config

```
/carpet fastRedstoneDust true
/carpet optimizedTNT true
```

Tweakeroo Configs

```
disableBlockBreakingParticles true
disableEntityRendering true
```



测试版本：20w16a

视频设定：图像品质：流畅，粒子效果：少量，渲染距离：10，1080p分辨率

测试平台：CPU: Athlon X4 860K GPU: GTX 960

树场版本：推出面积10\*24\*2 4gt  ver5.1

TPS: 20

MSPT: 20-25

FPS: 30-70 (视线对着电路部分会掉到30fps)



### <b>细节/注意事项</b>

- 防呆设计，开启农场的拉杆随意拉也不会弄坏机器。
- 关闭农场时，会自动先关闭<b>c<sub>1</sub>c<sub>2</sub>c<sub>4</sub></b>，再关闭<b>c<sub>3</sub></b>。防止bud状态的菌岩没有正确的收回。
- 矿车互相挤压的声音似乎也是bug，通过音量设置把音量调到最小然后再调到可以暂时解决这个问题。
- 注意控制电路都应尽量建造在树叶的生长范围以外。
- 开机前，记得在`input1`填充足够的盒装骨粉，让每个潜影盒卸载器至少有1盒装骨粉。`input2` 填充给足够的空潜影盒，让每个装盒器至少有一个潜影和在其缓存区。



## <b>花絮</b>

20w12a后从Rays Works的视频中得到灵感,有了做全自动树场的想法。于是后来发布了两个树场的设计，都是通过时钟控制活塞推动杂草，来刷新直到菌柄生成，不过一直不满足其效率。

如果想要提升效率，我首先想到的就是堆叠，如果能并排种复数的树那就好了。首先从两格宽的菌岩开始研究，不过没有改动架构，仍然用中继器检测式，缺点就是没有更多的空间继续堆叠更宽的树场。

直到从[20w12a 绯红菌/诡异菌树场 by Sela_Col](https://www.bilibili.com/video/BV1rE411P7eg) 得到灵感，可以做bud检测式的，发现bud检测式让堆叠成为可能。

尝试了多种，如水流式、向上推菌岩、相隔一格推地板等方式后。最后从ilmango的[BV1nE411c7k5](https://www.bilibili.com/video/BV1nE411c7k5) 得到灵感，这种方式或许时最好的选择。不过又面临新的问题，过多独立运行的时钟之间的配合极为复杂，怎样才能简单的布线也不失效率，我先降低各个时钟的频率，来测试这种架构的可能性。

研究发现，一种特定的bud装置，能非常智能地只在上方有实体方块时推出并收回。经过测试无论式菌柄还是疣块都能被检测到。同时猜想只要横向推动的活塞<b>p<sub>2</sub></b>与向上推的活塞<b>p<sub>1</sub></b>的周期相同，且<b>p<sub>2</sub></b>推出的时机，刚好是<b>p<sub>1</sub></b>推出之后，会因为推出的活塞无法被推动，就会解决加塞的问题。因此尝试着把<b>p<sub>1</sub></b>与<b>p<sub>2</sub></b>的相位错开，不过通过有限地知识理论来实践怎么都与猜想相悖。后来在胡乱调了一些延迟后，不下心就解决了问题，虽然不知道其中的原理。后来在农场建造完成后经过了一些研究，也就是上文[运作方式](#运作方式) 所写的。

20w15a更新了更多可以被堆肥的物品。同时我也完善了树场为其加上了基于潜影盒的物流系统，并新增疣块、地狱苗等杂草回授骨粉的功能。

从核心部件的设计，建造出第一个原型机，到发布视频前后断断续续经历了一周时间。

如果不是ilmango在20w15a的新闻视频中说，他将发布他的全自动树场，我还会多憋憋再发出来，赶着提前发出来一个预告。不过后来发现，无论是ilmango还是Rays works 的农场都是基于可自我回授的思路去设计的。

抱歉正式的视频鸽了这么久，一方面是忙其他事情去了，另一方面是这个农场还有诸多我不满意的地方，为了改进这些着实花了不少时间。

不过出系列视频的目也不仅仅是MC本身，也是为了熟悉各种工具、锻炼如何思考吧。



## <b>Q/A</b>

- <b>为什么建造这么高？</b>（指视频中巨大的玻璃罩子）

  由于巨型菌类的生长规则不同于其他的树木，即使菌类上方覆盖了方块，也能忽略方块成功生长。因此把无法处理的部分覆盖上玻璃，首先是防止多余的菌柄/疣块阻碍视线，另一个原因是，疣块有几率生成在红石线上方，从而切断红石线影响电路运行。

- <b>菌柄有什么用？</b>
  菌柄在Minecraft wiki 归类在原木的词条中，实际上的行为也与其它原木无异，除了它不能直接拿来作燃料，或者作为木炭的来源。但仍然可以合成为木棍来作为一种燃料的来源。

  经过测试20w16a暂时无法合成所对应的船的变种，不过我猜想，这是有意为之。如果能够被合成，这种防火的船会对赤足兽的存在产生威胁。
  
- <b>适用最新java版本吗？</b>

  发布这篇文章的时候，最新版本为20w17a可用，后续我会在标题上更新适用的版本号。

- <b>基岩版可以吗？</b>

  不行。

## <b>感谢</b>

### <b>灵感来源</b>

| 作者     | 标题                     | 链接         |
| -------- | ------------------------ | ------------ |
| Sela_Col | 20w12a 绯红菌/诡异菌树场 | [BV1rE411P7eg](https://www.bilibili.com/video/BV1rE411P7eg) |
| ilmango  |   芒果1.15树厂大合集     |[BV1A7411x7Fv](https://www.bilibili.com/video/BV1A7411x7Fv)|
|ilmango   |自动菌类农场 可切换模式    | [BV1uA411h7Cj](https://www.bilibili.com/video/BV1uA411h7Cj) |
|ilmango/Rays works|20w12a：强制催熟修复|[BV1eE411A75Z](https://www.bilibili.com/video/BV1eE411A75Z)|

### <b>使用部件</b>

| 作者         | 部件名称           | 链接                                                        |
| ------------ | ------------------ | ----------------------------------------------------------- |
| gpw          | 双倍速潜影箱填装器 | [BV16E411976J](https://www.bilibili.com/video/BV16E411976J) |
| SamosTheSage | 潜影盒装填/卸载    | [BV1CJ411a74R](https://www.bilibili.com/video/BV1CJ411a74R) |
| ilmango      | TNT 复制           | [BV1A7411x7Fv](https://www.bilibili.com/video/BV1A7411x7Fv) |
| ilmango      | 方块交换           | [av78346949](https://www.bilibili.com/video/av78346949/)    |
| ilmango      | 双倍速物品分类     | [av22580128](https://www.bilibili.com/video/av22580128)     |
| ilmango      | 50/50分类器        | [BV1qJ41167cN](https://www.bilibili.com/video/BV1qJ41167cN) |

### <b>推荐教程</b>

| 作者          | 作品标题                                               | 链接                                                        |
| ------------- | ------------------------------------------------------ | ----------------------------------------------------------- |
| 小渊xyz       | 【红石】活塞究竟是怎样伸出的？                         | [BV1LJ411E7Y4](https://www.bilibili.com/video/BV1LJ411E7Y4) |
| ilmango       | 【MC】0tick红石&瞬推活塞 原理&应用                     | [BV1sb411K7y6](https://www.bilibili.com/video/BV1sb411K7y6) |
| Donocean      | 【MC】想学0t？来这里就对了 最详细的0t原理讲解+干货讲解 | [av52246363](https://www.bilibili.com/video/av52246363)     |
| Fallen_Breath | 深度剖析Minecraft                                      | [cv4122119](https://www.bilibili.com/read/cv4122119/)       |



### <b>材质包</b> 

使用 <b>Xekr</b> 红石显示，同时感谢帮忙转发上个视频。



### <b>模组</b>

<b>gnembon: carpet, carpet extra</b>

<b>masady: minihud, itemscoller, tweakeroo, litematica, malilib</b>



## <b>附录</b>

### <b>物流</b>

[png](https://github.com/kagurakang/fully-automatic-fungus-tree-farm/blob/master/automatic%20fungus%20tree%20farm%20bone%20meal%20effe%20zh.png)



### <b>生产数据表格</b>

[pdf](https://github.com/kagurakang/fully-automatic-fungus-tree-farm/blob/master/fully%20automatic%20fungus%20tree%20farm%20bone%20meal%20effe%20zh%20v5.0.pdf)



### <b>存档与投影文件</b>

[地址]()

