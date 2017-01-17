
2016年 12月 06日 星期二 09:25:01 CST

1. 资讯模块分类标签栏；
2. 第一个标签内容栏；
3. 先用假数据完成；

4. 学习 git rebase 用法，用于整理当前提交内容；

study：

* AbListView 中的 setTextFilterEnabled 方法的[作用](http://blog.csdn.net/murongshusheng/article/details/7828119)

* 关于 ViewPager

  ViewPager viewpager = findViewById(R.id.view_pager);
  viewpager.setAdapter(new PagerAdapter());

PagerAdapter 的子类需要实现四个方法：
  1. instantiateItem(ViewGroup, int)
  2. destroyItem(ViewGroup, int, Object)
  3. getCount()
  4. isViewFromObject(View, Object)

第一个方法，ViewGroup.add(View)
第二个方法，ViewGroup.remove(View)
第三个方法，mViews.size()
第四个方法，View == Object

2016年 12月 06日 星期二 19:14:27 CST

1. 

2016年 12月 08日 星期四 07:59:22 CST

1. 增加落下下拉刷新和上拉加载更多功能；
2. 








