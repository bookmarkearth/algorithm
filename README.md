# 书签地球部分算法说明

## 首页算法
首页展示算法公示可能会导致用户作弊等不良后果，这里不做过多的披露。

## 首页文件夹展示（网页和APP端）

为了方便用户翻页和更大程度的呈现内容，系统在设计上将首页文件夹展示设置成为了左右翻页，这种做法并不是表象上的置顶行为，管理员也不会对展示结果做任何的干预。算法设计上首先会抽取一段时间内的用户上传的文件夹形成公平队列，然后采用WilsonScore Algorithm(威尔逊得分算法)交给用户来评选一段时间内相对优质的内容。

以下是sql语句实现的算法细节。

```
<!--置信度为95%,z=1.96的情况下的sql实现-->
 		(((bf.like_num+1) + 1.9208) / ((bf.like_num+1) + bf.dislike_num) - 1.96 * SQRT(((bf.like_num+1) * bf.dislike_num) / ((bf.like_num+1) + bf.dislike_num) + 0.9604) /         
      ((bf.like_num+1) + bf.dislike_num)) / (1 + 3.8416 / ((bf.like_num+1) + bf.dislike_num))
```

以上过程系统保持绝对的技术中立，不过由于考虑到文件夹展示位置相对显眼，系统需要更高的注意义务去清除不合法内容，所以系统会对可能存在
政治、色情、版权等内容的文件夹做屏蔽（也就是用户看到的加锁），阻止用户去点击。


## 违规内容过滤
这部分算法不适合公开，公开会导致大量的规避行为，所以暂时闭源。
