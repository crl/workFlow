## substance 学习资料
![Substance_Painter_Orc](https://support.allegorithmic.com/documentation/spdoc/files/20316164/170459743/2/1536351466340/Substance_Painter_Orc.jpg)
1. https://academy.substance3d.com/ 中文教材(点右上角中文)
2. prb引导文档(点右上角中文)
>* https://academy.substance3d.com/courses/the-pbr-guide-part-1
>* https://academy.substance3d.com/courses/the-pbr-guide-part-2
## pbr
>* [基于物理的渲染](http://mecg.me/wiki/doku.php?id=cg:pbr)
>* [GPU架构与渲染过程](http://mecg.me/wiki/doku.php?id=cg:gpu)
>* [demo/source](http://artisaverb.info/PBT.html)
##### 扩展
>* [Unity的PBR扩展](https://zhuanlan.zhihu.com/p/50822664) [git](https://github.com/chenyong2github/ExtendStandard)


## 换肤/捏脸/调色/换装
##### 捏脸
1. uma方案 
> https://www.youtube.com/playlist?list=PLkDHFObfS19zFVfbrfB14P-u5QJJQyvtP
>* 换装 (格位,是否替换其它格位或部件,是否隐藏其它格位或部件,包含顶点mask)
>* 整体换(如变身)
>* 换色
>* 捏骨骼
>* 等等 单纯看演示的话 考虑的挺周到的,并且接合也合理
2. 天刀的说明 
>* http://games.sina.com.cn/o/z/wuxia/2015-10-15/fxivsch3599438.shtml
3. ue4 《Honey Select》捏人剖析
>* https://zhuanlan.zhihu.com/p/28471808

##### 表情
1. Blend Shapes (由dcc工具导出,skinMesh.SetBlendShapeWeight)
>* https://zhuanlan.zhihu.com/p/58631750

##### 调色
1. hsv
>* https://zhuanlan.zhihu.com/p/52147126
```shaderlab
half bias = 0.1f;
half4 mask = tex2D(_RecolorMask, uv);
int maskIndex = (int)(step(bias, mask.r)
	+ step(bias, mask.g) * 2
	+ step(bias, mask.b) * 4);
	
//使用hsv进入混色	
DyeColor = HSV2RGB (RGB2HSV(BaseColor) + HSVOffset)
```
## Human
1. ue4中的
>* https://docs.unrealengine.com/en-us/Engine/Rendering/Materials/HowTo/Human_Skin 
>* https://docs.unrealengine.com/en-us/Resources/Showcases/PhotorealisticCharacter
>* https://docs.unrealengine.com/en-us/Resources/Showcases/DigitalHumans
2. https://renderman.pixar.com/louise
3. https://developer.nvidia.com/gpugems/GPUGems3/gpugems3_ch14.html 
4. https://80.lv/articles/secrets-of-human-shaders-in-ue4/ 一个美术ue4里的,但我觉得主要还是画的好
5. [lux.git 源码](https://github.com/larsbertram69/Lux/tree/master/Lux%20Shader/Human)

##### 皮肤
>* 油脂层
>* 透光性
>* 皮肤泛红
>* SSS
>* 核心主要是皮肤要分清楚,把漫反射的阴影替换成血色过渡,再加一个次表面散色,最后一个模糊权重过渡
##### 头发
>* 高光切线法 双层高光 透明度 AlphaTest 做多次的pass
>* [UnityHairShader.git](https://github.com/AdamFrisby/UnityHairShader)
1. [Kajiya切线高光法.pdf](http://web.engr.oregonstate.edu/~mjb/cs519/Projects/Papers/HairRendering.pdf)
```shaderlab
//对切线在法线方向上进行偏移
float3 ShitTangent(float3 T,float3 N,float shift){
  float3 shiftedT=T+shift*N;
  return normalize(shiftedT);
}
```
2. 延伸 https://developer.nvidia.com/gpugems/GPUGems2/gpugems2_chapter23.html 加了物理
3. 延伸[NVIDIAHairWorksIntegration.git](https://github.com/unity3d-jp/NVIDIAHairWorksIntegration)
##### 眼睛
>分层
>* 瞳孔
>* 眼白
>* 泪腺
>* 角膜(高光)
>* 睫毛
1. [substance源文件](https://share.substance3d.com/libraries/2432)
##### 布料
>* [ClothParticlePhysics.git](https://github.com/jackisgames/ClothParticlePhysics)
>* [Cloth-Simulation.git](https://github.com/danielshervheim/Cloth-Simulation)
1. 相应的节点约束 (线性权重)
2. 碰撞约束

## ik
>* https://docs.unity3d.com/Manual/InverseKinematics.html
##### 约束
>* https://docs.unity3d.com/Packages/com.unity.animation.rigging@0.2/manual/index.html)
1. 武器收起与脱手 (不同的父级,动态调整权重)
2. 其它 (我感觉其它的比较次要)

##### 动作状态机
1. 可调整动作衔接时间及条件组合
2. 切换优化级
3. [AvatarMask](https://docs.unity3d.com/Manual/AnimationLayers.html) 上下身分离 (边跑 边跳 边表情 边招手等)
4. [Retargeting](https://zhuanlan.zhihu.com/p/25064011) 动画重定向技术
5. [TargetMatching](https://docs.unity3d.com/Manual/TargetMatching.html) 动作与位置的对齐操作(如翻墙,美术是做了个动作，但墙位置及高度会有所不同)

##### 爬墙
>https://www.youtube.com/playlist?list=PL47vwJBRNh1xzEvcLvXoJvjLcr1h0j-1O
##### 游泳
##### Ragdoll
1.工具化



## [镜头](https://docs.unity3d.com/Packages/com.unity.cinemachine@2.3/manual/index.html) 角色控制器
1. [基本 镜头](https://docs.unity3d.com/Packages/com.unity.cinemachine@2.3/manual/CinemachineFreeLook.html) CinemachineFreeLook 可设置穿透遮挡体
2. [状态 镜头](https://docs.unity3d.com/Packages/com.unity.cinemachine@2.3/manual/CinemachineStateDrivenCamera.html) (由于动作的不同镜头的推进拉远等)

## 场景
1. navmesh 分层:雪地/草地/水面 (导出给服务端使用,一般是导出高度图:(x,z的 y的高度),主要定位脚的位置)
2. collider 物理碰撞(寻路navmesh可以做,但飞行跳跃 落点 有collider可做更细致的内容)
3. 区域编辑 (进入触发,如天气变化,镜头等,一般会触发一个skill.amf文件,由技能编辑器产出)
4. 剧情
5. npc/monster 定位
6. 草/水/风/粒子系统 动有东西
7. 触发关联 (如门与机关)

## 天气系统
1. 时间变化 (白天黑夜)
2. 天气变化 (风雨雷电,地表有积水,地表被雪覆盖)
3. 等等

## 交互草
>* [GrassProject.git](https://github.com/toninhoPinto/GrassProject)

## 水
##### 水
>* [Optically-Realistic-Water.git](https://github.com/muckSponge/Optically-Realistic-Water)
1. 有深度差别
2. 有水面下的扭曲
3. 泡沫
4. 是否有交互
5. 顶点动画
##### flowmap
1. [photoshop生成](https://www.unrealengine.com/zh-CN/blog/photoshop-generated-flow-maps?lang=zh-CN&sessionInvalidated=true),当参考
2. 另类 [做高光的各向异性](https://mp.weixin.qq.com/s?__biz=MzIyMzQzNDAyNg==&mid=2247484087&idx=1&sn=b2fa7f5af318785e72cd9428776093f8&chksm=e81f06f2df688fe441a4c7a6db229b69bbcd3de23a07e59670e8a97d41765b1be099e2e7a6cd&scene=21#wechat_redirect)
3. [substance制作](https://support.allegorithmic.com/documentation/spdoc/flow-map-painting-143327274.html)
##### unity内部
>* https://docs.unity3d.com/Manual/HOWTO-Water.html 可以当做参考
##### assetStore (已买的)
>* https://assetstore.unity.com/packages/vfx/shaders/realistic-water-33434 可交互
>* https://assetstore.unity.com/packages/vfx/shaders/suimono-water-system-4387

## 场景效果
1. linear space
2. 烘培
3. HDRI 天空球
4. Reflection Probe 来增加反射效果，也可用它来区分环境
5. Light Probe 来做动态物体的间接光
6. emission 调hdr色
7. [Postprocessing](https://docs.unity3d.com/Packages/com.unity.postprocessing@2.1/manual/index.html) 主要为(bloom/Lut) 
>* [光照介绍](https://learn.unity.com/tutorial/intermediate-lighting-rendering)
>* 一个铁道的[demo内含源码](https://unity3d.com/learn/tutorials/s/creating-believable-visuals?_ga=2.257319819.1060887464.1557711885-1438279476.1522757191)
>* [更好光线的7个小提示](https://lmhpoly.com/7-tips-for-better-lighting-in-unity/) 
>* 自动Light Probe [说明](https://blog.csdn.net/noligz/article/details/54916045) [git](https://github.com/gampixi/auto-light-probes)

## 场景优化方案
1. 遮蔽 (Occlusion culling)
2. subScene
4. 研究:是否有Scene存在的必要,如果没有,需自己记录lightmap信息,动态9宫加载lightmap(收集由mesh的lightmapIndex)
>[lightmap拆分](https://www.cnblogs.com/fishyu/p/7703812.html)
5. 开关投/接 阴影 反射球 等， 是否有必要动态合并(使文件变大,如果做超大场景 就会浪费很多很多的东西)
6. 阴影级数 尽量降级2层
7. lod 是否有必要 (理论上是超必要)
8. 资源 read/write 关闭 mip级数
9. 粒子系统 现在有默认关闭的（自动优化镜头内）
10. 是否有合并贴图的必要 （小物件合一起）


## 角色打光
1. 镜头光
2. Light Probe 动态取改 [LightProbeEditor.git](https://github.com/chenjd/LightProbeEditor)
3. sh9/vertexLight

## 剧情
>由timeLine完成,cinemachine来做镜头 Postprocessing做区域镜头特效

## 犯的错误
 1. 对场景进行了静态合并 (research: StaticBatchingUtility进行运行时合并)
  * 对于共用资源 产生了多份的合并资源 内存增大
  * 对于ab打包，也产生了Scene特大问题
  * 对资源需开启read/write
 2. 自动打包功能无法预览 (research:AbBrowse结合,再用AssetStudio查看什么东西比较大)
 3. 抽出了lightmap独立打 会使lightmap无效
 4. shader variants 太多 太大问题
 10. and so on
  
 ## 技巧性方案
 * 对美术与程序分离
 * 分代码库 把需要绑定到gameObject上的独立库,把程序应用独立成库,这样基本的dll热更新 可直接在手机上热更新调试
 * 做远程发布 逻辑代码dll,及assetbundle 服务,
 * unity插件 svn tools lite unity上直接提交svn ,[ConsoleE]更方便调试调用堆栈
 * 
 
 
  
## unity扩展编辑器
>* https://www.youtube.com/playlist?list=PLs023Yclit4nom70pyx0wIxQLWf4Q7nIU
>* https://anchan828.github.io/editor-manual/web/ 一日本人写的书
