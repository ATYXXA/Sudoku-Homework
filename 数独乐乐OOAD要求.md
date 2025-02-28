# 数独乐乐 OOAD

逆向分析现有数独项目的面向对象技术，然后按新业务愿景，改进升级为数独乐乐应用；分析、设计出面向对象技术方案，并落地代码实现。

现有数独项目：https://github.com/jonasgeiler/sudoku

![image-20241117084341694.png](https://rain-oplat.xuetangx.com/ue/2024-11-17/64913297/1731817947623-image-20241117084341694.png)



## 逆向分析

逆向工程，对现有项目的OOA、OOD、OOP进行分析：

1. 讨论其设计思想、设计原则和使用的设计模式，给出其**愿景**、**用例分析**、**领域模型**、**技术架构**与**对象模型**；
2. 结合课程，评价现有OOD架构与设计的优劣，给出**改进建议**。

## 新业务愿景

升级应用为**数独乐乐**。让游戏更加适合初学者，给用户更多友好指引。同时，集成SudokuWiki.org，便于持续提升求解算法和验证开发。

### 下一步提示

通过提示按钮，为用户提示下一步可以选择的答案，并提示线索，说明推理答案所用的方法（策略）。

![image-20241117111654841.png](https://rain-oplat.xuetangx.com/ue/2024-11-17/64913297/1731818040873-image-20241117111654841.png)

### 探索回溯

方便用户在多种可能得答案中，漫游、探索、回溯

![image-20241117114925300.png](https://rain-oplat.xuetangx.com/ue/2024-11-17/64913297/1731818109516-image-20241117114925300.png)

### 资源集成

集成数独Wiki资源，包括题目、算法策略。 https://www.sudokuwiki.org/Sudoku.htm

#### 题目导入

能够将数独Wiki的题目页的URL作为Code，直接导入到数独乐乐中使用。

![image-20241117112637984](https://fe-static-yuketang.yuketang.cn/fe/static/js/ueditor/themes/default/images/spacer.gif)![image-20241117112637984.png](https://rain-oplat.xuetangx.com/ue/2024-11-17/64913297/1731818143036-image-20241117112637984.png)

#### 算法策略

给出良好的OOAD，能够高效、正确地在**数独乐乐**中引入、集成数独Wiki的各种算法策略。重点在于，

1. 如何验证策略算法正确性；
2. 如何在确保算法独立性，即新算法的引入不会影响老算法的正确性，也不会降低老算法的与性能。

![image-20241117112905334.png](https://rain-oplat.xuetangx.com/ue/2024-11-17/64913297/1731818170754-image-20241117112905334.png)



