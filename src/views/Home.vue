<template>
  <div>
    <div class="body">
      <h1>遗传算法求解TSP</h1>
      <h3>满足故障根因定位实时性的要求</h3>
      <h3>可视化展现根因信息及根因关联的局部拓扑图</h3>
      <div class="blank"></div>
      <!-- <span id="1" />
      <a-affix :offset-top="top">
        <a-menu v-model="current" mode="horizontal">
          <a-menu-item key="mail">
            <a href="#1">
              <a-icon type="read" />算法说明
            </a>
          </a-menu-item>
          <!-- <a-menu-item key="app">
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
            赛题背景为大型电商平台内部大量系统之间的互相调用时会产生大量告警数据，
            <br />我们需要找出有效告警以及疑似根因的告警，解决网络运维面临的主要难题。
            <br />赛题主要涉及数据分析、图论、信息论、自然语言处理、神经网络等技术，
            <br />要求队员掌握相关的基础知识，具有python数据分析、处理及功能开发能力。
            <br />合作完成的系统应准确、快速的定位网络故障，提升一线网络运维的效率，降低网络故障产生的损失。
          </p>
          <p>
            <b>赛题要求实现以下各部分功能:</b>
            <br />1、过滤无效告警，即做到对告警数据进行去噪。
            <br />2、挖掘不同告警信息之间的关系，即做到对告警信息聚类。
            <br />3、对类内告警信息进行因果关系匹配，进一步缩小范围，确定根因。
          </p>
          <p>
            <b>系统设计及功能要求如下：</b>
            <br />1、要求能可视化展现根因信息及根因关联的局部拓扑图。
            <br />2、要求系统运行稳定、可靠、流畅。
            <br />3、系统设计要求目录结构设计合理。
            <br />4、功能模块划分合理。
            <br />
            <span id="2" />
            5、代码要求整洁，易读，符合程序编码规范，命名规范，注释清楚。
            <br />
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
  height: 1500px;
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
}
hr {
  color: rgba(0, 0, 0, 0.5);
}
#question {
  background: #fff url(./img/1.png) no-repeat top right;
  height: 400px;
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