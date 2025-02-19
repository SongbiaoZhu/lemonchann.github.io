---
layout: post
title: "sublime regrex 提取中文段落及正则替换为markdown格式"
date:   2022-04-16
tags: [regrex]
 
comments: true
author: Songbiao Zhu
---

为了整理美国五大地区的主要大学分布信息，[本网页]有内容，但是不能复制，不间断跳出广告，所以可以通过正则表达式整理出关键部分的内容，以markdown格式呈现。

<!-- more -->

## 主要步骤

1. 网页源代码复制，截取包含有用信息的源代码部分
2. 从网页源代码中正则提取所有中文段落
3. 将中文段落中的子标题正则查找和替换为 ## 加段落标题
4. 另存text文档为markdown格式.md 。 完成。


首先，
查找所有的中文段落
`[^\x00-\xff]+`

sublime 正则查找替换
查找如下
`(.+地区\s)`
 替换如下
`## $1`

sublime 正则查找替换
查找如下
`大学：**`
 替换如下
`**$1**`

整理完的内容如下：
## 新英格兰地区

新英格兰地区，这个地区一共包括缅因州、新罕布什尔州、佛蒙特州、马赛诸塞州、康涅狄格州和罗德岛州。主要的城市包括波士顿、普罗维登斯、哈特福德。
新英格兰地区面积不大但是土壤肥沃，十九世纪是当时全国的文化经济中心，大片的可耕种土地与南方地区非常不同。不过现在该地区的主体行业已经转为造船、捕鱼及贸易。这里还形成了规模巨大的布匹、来复枪、钟表等制造业。近年来，随着微电子、教育、高科技、金融服务、旅游、医药、电脑及生物技术等行业的发展，这一地区的经济回升迅速，也提供了大量的相关工作机会。
**推荐大学：**
缅因大学、哈佛大学、麻省理工大学、波士顿大学、波士顿学院、东北大学、塔夫斯大学、布兰迪斯大学、布朗大学、耶鲁大学。

## 大西洋沿岸地区

纽约州、新泽西州、宾夕法尼亚州、特拉华州、马里兰州。主要城市包括纽约、费城、巴尔迪莫。
十九世纪这个地区是生产铁、玻璃、钢材的重工业中心。随着重工业在这个地区的扩展，经济飞速发展，纽约至今仍是美国最大的城金融枢纽及文化中心。著名的西点军校和海军学院都在这个地区，反映出大西洋沿岸地区的历史重要性。随着时间的退役，这个地区大部分重工业已经搬迁，取而代之的是制药和通信行业以及服务行业，这些行业的兴起也为药理学、医学、
、商科等专业毕业生提供了很多新的工作岗位。
**推荐大学：**
哥伦比亚大学、康奈尔大学、纽约大学、罗切斯特大学、伦斯勒理工学院、雪城大学、宾夕法尼亚大学、卡耐基梅龙大学、宾州州立大学、匹兹堡大学、马里兰大学、佩斯大学。

## 南部地区

佛吉尼亚州、西佛吉尼亚州、肯塔基州、田纳西州、北卡罗来纳州、南北卡罗来纳州、佐治亚州、佛罗里达州、阿拉巴马州、密西西比州、阿肯色州、路易斯安那州、德克萨斯州，包含的主要城市有亚特兰大、新奥尔良、夏洛特、迈阿密、纳什维尔、休斯顿。
除了总统里根以外，历任总统均出自高低区。卡特总统在佐治亚、布什父子在德克萨斯、克林顿来自阿肯色。总统效应下，南方吸引了众多的国际活动和大量的投资人，时至今日，南方已经演变成制造、银行、运输诸业兴旺发达的地区。由于气候温和，南方十分适宜居住生活。这是还是文学氛围最浓厚的地区，尤其是在二十世纪，包括威廉
福克纳描写密西西比生活的长篇小说，田纳西
威廉的剧作以及弗兰纳里
奥康纳的短篇小说都诞生于此。
**推荐大学：**
佐治亚理工、阿肯色州立大学、佛罗里达大学、佛罗里达州立大学、田纳西大学、德州大学奥斯丁分校、莱斯大学、德州农工大学、迈阿密大学。

## 中西部地区

中西部包含俄亥俄州、密歇根州、印第安纳州、威斯康辛州、伊利诺伊州、明尼苏达州、爱荷华州、北达科他州、南达科他州、堪萨斯州、内布拉斯加州、密苏里州、奥克拉荷马州。包含的主要城市有克利夫兰、底特律、芝加哥、明尼阿波利斯、圣路易斯。
密西西比河是这个地区的生命线，马克
吐温在这里发表了两步美国名著——《密西西比河上的生活》和《哈利贝利
费恩历险记》还有莫里森、海明威、桑德伯格、休息、安热卢都成名于此。这里还有有全国最大城市芝加哥和著名的汽车城底特律。工业发达的中西部为理工科的学生提供了很多就业机会同时他们的居民又酷爱文学。
**推荐大学：**
堪萨斯大学、俄亥俄州立大学、印第安纳大学、威斯康辛大学麦迪逊分校、伊利诺里大学香槟分校、明尼苏达大学双城分校、华盛顿大学圣路易斯分校、内部拉斯大学林肯分校。

## 西部地区

西部包含：新墨西哥州、亚利桑那州、科罗拉多州、怀俄明州、蒙大拿州、犹他州、加州、内华达州、爱达荷州、俄勒冈州、华盛顿州、阿拉斯加州、夏威夷州。主要城市包括洛杉矶、旧金山、丹佛、菲尼克斯、阿尔伯科尔基、圣菲、檀香山。
西部地域辽阔、风景如画、壮阔非凡。美国第二大的城市洛杉矶坐落于此，好莱坞的电影业称霸世界，这个地区是非适宜居住，可与南部媲美。圣菲和陶斯是世界闻名的艺术中心，尤以油画、雕塑及歌剧著称，简单的来说，这里是艺术生的天堂。西部人以宽容著称，对外国人非常友好，他们形容自己的人际关系是“自己活也让别人活”。
**推荐大学：**
加州大学洛杉矶分校、加州大学圣巴巴拉、旧金山艺术学院、旧金山大学、亚利桑那州立大学、夏威夷大学、犹他大学。