<template>
  <div>
    <div class="body">
      <h1>遗传算法求解TSP</h1>
      <h3>满足遗传算法求解TSP实时性的要求</h3>
      <h3>可视化展现</h3>
      <div class="blank"></div>
      <!-- <span id="1" />
      <a-affix :offset-top="top">
        <a-menu v-model="current" mode="horizontal">
          <a-menu-item key="mail">
            <a href="#1">
              <a-icon type="read" />算法说明
            </a>
          </a-menu-item>
          <a-menu-item key="app">
            <a href="#2">
              <a-icon type="read" />使用说明
            </a>
          </a-menu-item> 
          <a-menu-item key="alipay">
            <a href="#us">
              <a-icon type="smile" />成员分工
            </a>
          </a-menu-item>
        </a-menu>
      </a-affix> -->
      <div class="content">
        <div id="question">
          <h2>算法说明</h2>

          <p>
            &nbsp;&nbsp;遗传算法（ genetic algorithm (GA) ）是计算数学中用于解决最优化的搜索算法，
            <br />是进化算法的一种。进化算法最初是借鉴了进化生物学中的一些现象而发展起来的，
            <br />这些现象包括遗传、突变、自然选择以及杂交等等。

            
          </p>
          <p>
            <b>遗传算法实现方式</b>
            <br />&nbsp;&nbsp;遗传算法通常实现方式为一种计算机模拟。对于一个最优化问题，
            <br />一定数量的候选解（称为个体）可抽象表示为染色体，使种群向更好的解进化。
            <br />传统上，解用二进制表示（即0和1的串），但也可以用其他表示方法。
            <br />进化从完全随机个体的种群开始，之后一代一代发生。在每一代中评价整个种群的适应度，
            <br />从当前种群中随机地选择多个个体（基于它们的适应度），通过自然选择和突变产生新的生命种群，
            <br />该种群在算法的下一次迭代中成为当前种群。 
          </>
          <p>
            <b>TSP介绍：</b>
            <br />&nbsp;&nbsp;TSP是旅行购买者问题与车辆路径问题的一种特殊情况。

            <br />作为计算复杂性理论中的一个典型的判定性问题，TSP的一个版本是给定一个图和长度 L，
            <br />要求回答图中是否存在比 L 短的回路（英语：circuit或tour）。该问题被划分为NP完全问题。
            <br />已知TSP算法最坏情况下的时间复杂度随着城市数量的增多而成超多项式（可能是指数）级别增长。

            <br />问题在1930年首次被形式化，并且是在最优化中研究最深入的问题之一。许多优化方法都用它作为一个基准。
            <br />尽管问题在计算上很困难，但已经有了大量的启发式和精确方法，因此可以完全求解城市数量上万的实例，
            <br />并且甚至能在误差1%范围内估计上百万个城市的问题。
          </p>
        </div>
        <hr />
        
        <div id="us">
          <div class="right">
            <h2>成员分工</h2>
            <p>
              <b>队长：</b>荣鹏
              <br />负责后端框架以及遗传算法的设计与编写
            </p>
            <p>
              <b>队员1：</b>胡锦龙
              <br />负责前端代码编写以及数据的可视化展现
            </p>
            <p>
              <b>队员2：</b>董文睿
              <br />负责算法分析以及系统设计评估
            </p>
          </div>
        </div>
      </div>
      <a-back-top />
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      current: [""],
      top: -5,
      bottom: 10
    };
  }
};
</script>
<style>
.body {
  background: #fff url(./img/bg1.png) no-repeat top right;
  background-size: 600px 596px;
  height: 1300px;
}
.body h1 {
  font-size: 36px;
  position: relative;
  top: 168px;
  left: 50px;
}
.body h3 {
  position: relative;
  left: 70px;
  top: 180px;
}
.blank {
  height: 400px;
}
.content {
  position: relative;
  top: 10px;
  letter-spacing: 3px;
}
.right {
  float: right;
  margin-right: 150px;
  margin-top: 50px
}
.bla:before {
    content : "\2003\2003";
}
hr {
  color: rgba(0, 0, 0, 0.5);
}
#question {
  background: #fff url(./img/1.png) no-repeat top right;
  height: 450px;
  background-size: 1000px 500px;
}
#use {
  background: #fff url(./img/foruse.png) no-repeat top center;
  height: 3000px;
  background-size: cover;
}
#us {
  background: #fff url(./img/big.png) no-repeat left;
  height: 284px;
  background-size: 593px 284px;
}
</style>