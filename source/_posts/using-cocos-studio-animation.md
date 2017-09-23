---
title: 使用cocos studio制作动画
categories: cocos2dx
tags:
  - cocos studio
  - cocos2dx
  - animation
date: 2017-08-04 20:46:02
---
## 概述
虽然触控不维护cocos studio了，但是很多人却还在使用着，比如我们公司就还用着，因为需要做动画。但是我不会，只会代码去写动画，太费时间了有没有啊，所以就决定去研究下怎么用编辑器去做动画了。现在把过程记录下来，以便日后复习。
<!-- more -->
## 动画只是简单的移动、旋转淡入淡出等简单的动画，创建步奏如下：
1. 首先新建一个节点，见下图：
{% asset_img 1.png %}
{% asset_img 2.png  %}
2. 拖一个Text控件到我们刚创建的节点上面。然后我们就可切入正题开始做动画了。
3. 点击“+”号创建一个动画
{% asset_img 3.png  %}
点击“+”后会弹出一个对话框，如下
{% asset_img 4.png  %}
4. 动画创建好了，我们可以开始编辑动画了。这里我们使用自动记录动画的功能这样比较方便。按钮在这里啦
{% asset_img 5.png  %}
选择“开始记录动画”以后我们就可以开始编辑动画效果了。这里我们就让文字旋转360°吧。
（1）首先第一帧不用管，直接插入关键帧就好了。
（2）将插入位置移动到下一帧，然后修改旋转属性为“90°”
{% asset_img 6.png  %}
重复循环这一步骤，直到Text文字变换回到开始位置（0°）
5. 取消勾选“开始记录动画”，到这里旋转动画就完成了。我们可以点击播放按钮看看效果。
{% asset_img 7.png  %}
6. 有人肯定会问，那我们开始创建动画的时候填的名字有什么用呢。哈哈，不用急我的理解是当我们有多个动画的时候，名字就可以派上用场了。举个例子，有个角色有三个动画分别是“run”、“walk”和“attack”。我们在制作的时候就可以这么去做了。
（1）0-20帧我们制作“run”的动画，动画的名字就叫做“run”。
（2）25-45帧我们制作“walk”的动画，动画的名字就叫做“walk”。
（2）50-70帧我们制作“attack”的动画，动画的名字就叫做“attack”。
聪明的你是不是已经明白一切了。就是你想的那样。我们在代码中可以通过名字来播放相应的动画。是不是比用帧去播放容易记点呢。

## 用图片制作动画

1. 很简单导入资源，你只需要选择好你需要的资源，然后把它拖入到cocos studio左下角的项目窗口就可以了。
2.创建一个新的节点，然后在节点上新创建一个精灵。 
3. 在项目选择你需要的资源直接拖到我们刚创建的精灵上。好了大工告成，是不是很简单呢？
{% asset_img jdfw.gif  %}

## 发布资源
1. 在发布资源之前记得把我们创建的两个节点放到场景中去。
{% asset_img 9.png  %}
2. 当编辑好了动画就可以发布了。因为们这里没有有新建vs工程所以这里我选择发布vs工程，然后并打开它。
{% asset_img 8.png  %}

## 代码播放动画
1. 在`HelloWorld::init()`中添加如下代码：
``` c++
	ActionTimeline* action1 = CSLoader::createTimeline("spite1.csb");
	rootNode->getChildByName<ui::Text*>("sprite1")->runAction(action1);

	ActionTimeline* action2 = CSLoader::createTimeline("spite2.csb");
	rootNode->getChildByName<Sprite*>("sprite2")->runAction(action2);
	action1->gotoFrameAndPlay(0, true);

	//action1->play("ani2",true);
	action2->gotoFrameAndPlay(0, true);
```
2. 好了，到现在为止，本教程就全部讲完了，按下`F5`看看效果吧。下面是我的效果：
{% asset_img runScreen.gif  %}

