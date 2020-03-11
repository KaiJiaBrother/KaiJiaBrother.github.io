---
title: Tableau
abbrlink: 9c9742d
date: 2020-03-11 10:10:24
tags:
---
1. Create a Top N Filter顺序问题
From the Data pane, drag City to the Filters shelf：filter的City还是原数据里的所有City，不是通过filter State之后的City(top N filter or the set filter排序问题)
原因：Tableau Order of Operations(the order that Tableau performs various actions, such as the order in which it applies your filters to the view.)

解决方法：On the Filters shelf, right-click the Inclusions (Country, State) (Country, State) set and select Add to Context.




Reference:
1. [help.tableau.com](https://help.tableau.com/current/guides/get-started-tutorial/en-us/get-started-tutorial-drilldown.htm)
