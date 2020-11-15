<template>
<div>
  <div class="amap-page-container">
      <el-amap vid="amapDemo" :zoom="zoom" :center="center" class="amap-demo" :events="this.events">
        <el-amap-marker vid="component-marker" :position="componentMarker.position" :content-render="componentMarker.contentRender" ></el-amap-marker>
        <el-amap-marker v-for="(marker, index) in markers" :position="marker.position" :events="marker.events" :visible="marker.visible" :draggable="marker.draggable" :vid="index" ></el-amap-marker>
        <el-amap-polyline :editable="polyline.editable"  :path="polyline.path" :events="polyline.events" ></el-amap-polyline>
      </el-amap>
      <div class="toolbar"> 
        <a-table :pagination="false" :columns="columns" :data-source="data" :scroll="{ y: 300 }" style="width: 300px; height: 380px">
        <a slot="name" slot-scope="text">{{ text }}</a>
        </a-table>
        <div class="paras">
        <a-row>
      <a-col :span="12">
        <span>迭代遗传数：</span>
        <a-slider v-model="inputValue1" :min="10" :max="5000" />
      </a-col>
      <a-col :span="4">
        <a-input-number v-model="inputValue1" :min="10" :max="5000" style="marginLeft: 16px" />
      </a-col>
    </a-row>
    <a-row>
      <a-col :span="12">
        <span>遗传个体数：</span>
        <a-slider v-model="inputValue2" :min="10" :max="1000" />
      </a-col>
      <a-col :span="4">
        <a-input-number v-model="inputValue2" :min="10" :max="1000" style="marginLeft: 16px" />
      </a-col>
    </a-row>
    <a-row>
      <a-col :span="12">
        <span>变异率</span>
        <a-slider v-model="inputValue" :min="0" :max="1" :step="0.01" />
      </a-col>
      <a-col :span="4">
        <a-input-number
          v-model="inputValue"
          :min="0"
          :max="1"
          :step="0.01"
          style="marginLeft: 16px"
        />
      </a-col>
    </a-row>
  </div>
        <a-button  name="button" v-on:click="removeMarker">remove marker</a-button>
        <a-button type="primary" name="button" v-on:click="result" :disabled="disabled">result</a-button>
      </div>
      
  </div>
    
</div>
    
</template>

  <style>
  .amap-page-container{
    height: 570px;
    width: 920px;
  }
  .toolbar{
    position: relative;
    top: -570px;
    left: 930px;
  }
  .code-box-demo .ant-slider {
  margin-bottom: 16px;
  }
  .paras{
    width:300px;
    margin-bottom: 8px;
    /* position: relative;
    float: right;
    top: -250px; */
  }
  </style>

  <script>
 
  const columns = [
  
  {
    title: '生成结果时间',
    dataIndex: 'time',
    key: 'time',
    width: 80,
  },
  {
    title: '最优路径距离',
    dataIndex: 'length',
    key: 'length',
    ellipsis: true,
  },
  
  
];
    const data = [];
    const exampleComponents = {
      props: ['text'],
      template: `<div>text from  parent: {{text}}</div>`
    }
    module.exports = {
      name: 'Analyze',
      data() {
        return {
          disabled: false,
          data,
          columns,
          key: 1,
          time: null,
          result_distance: null,
          inputValue: 0,
          inputValue1: 10,
          inputValue2: 10,
          count: 1,
          websock: null,
          slotStyle: {
            padding: '2px 8px',
            background: '#eee',
            color: '#333',
            border: '1px solid #aaa'
          },
          zoom: 5,
          center: [100.5273285, 38.21515044],
          events: {
            'click': (e) => {
              if(this.markers.length <= 30 ){
                //alert(e.lnglat);
              let marker = {
              position: [e.lnglat.lng, e.lnglat.lat]
              };
              this.markers.push(marker);
            }else{
            this.$message.error('标点过量！！请不要超过25个');
          }
            }
          },
          markers: [                                                    //标记数组
            {
              position: [100.5273285, 38.21515044],
              events: {
                click: () => {
                alert('click marker');
                }
              },
              visible: true,
              draggable: false,
              template: '<span>1</span>',
            }
          ],
           polyline: {
            path: [],     //路线
            events: {
              click(e) {
                alert('click polyline');
              },
              end: (e) => {
                let newPath = e.target.getPath().map(point => [point.lng, point.lat]);
                console.log(newPath);
              }
            },
            editable: false
          },
          renderMarker: {
            position: [100.5273285, 38.21515044],
            contentRender: (h, instance) => {
              // if use jsx you can write in this
              // return <div style={{background: '#80cbc4', whiteSpace: 'nowrap', border: 'solid #ddd 1px', color: '#f00'}} onClick={() => ...}>marker inner text</div>
              return h(
                'div',
                {
                  style: {background: '#80cbc4', whiteSpace: 'nowrap', border: 'solid #ddd 1px', color: '#f00'},
                  on: {
                    click: () => {
                      const position = this.renderMarker.position;
                      this.renderMarker.position = [position[0] + 0.002, position[1] - 0.002];
                    }
                  }
                },
                ['marker inner text']
              )
            }
          },
          componentMarker: {
            position: [100.5273285, 38.21515044],
            contentRender: (h, instance) => h(exampleComponents,{style: {backgroundColor: '#fff'}, props: {text: 'father is here'}}, ['xxxxxxx'])
          },
          slotMarker: {
            position: [121.5073285, 38.21515044]
          }
        };
      },
      computed:{
          sendmess:function(){
            let a = [];
            this.markers.forEach(function(element) {
            a.push(element.position);
          });
            return a;
        }
      },
      created() {             //由页面创建时初始化socket改为点击result再初始化？？没成功
      createSocket('ws://192.168.1.102:8000')
      },
      destroyed() {
      //this.websock.close() //离开路由之后断开websocket连接
      },
      methods: {
        onClick(e) {
          this.count += 1;
        },
        removeMarker() {
          if (!this.markers.length) return;
          this.markers.splice(this.markers.length - 1, 1);
          this.polyline.path = [];
        },
        result: function(){
          //this.openNotificationWithIcon('success');
        if(this.markers.length >= 5){
          this.disabled = true;
          this.$axios
        .post("http://192.168.1.102:8000/input/", {
          data: this.sendmess,
          max_generation: this.inputValue1,
          population_size: this.inputValue2,
          p_mutation: this.inputValue,
        })
        .then(response => {
          this.polyline.path = response.data.result;
          this.time = response.data.time;
          this.result_distance = response.data.result_distance;
          let ress = {
            key: '' + this.key++,
            time: '' + this.time,
            length: ''+this.result_distance
          }
          this.data.push(ress);
          //this.openNotificationWithIcon('success');
          this.disabled = false;
        })
        .catch(error => {
          //console.log(error);
          this.disabled = false;
          this.$message.error(error.response.data.detail);
          //console.log(error.response.data.detail);
        });
        this.way2 = 'result';
        }else{
          this.$message.error('标点数量须大于5！！');
        }
        
        },
        //以下是vue-socket
        
      //   initWebSocket(){ //初始化weosocket
      //   const wsuri = "ws://192.168.1.102:8000";                      //后端接口
      //   this.websock = new WebSocket(wsuri);
      //   this.websock.onmessage = this.websocketonmessage;
      //   this.websock.onopen = this.websocketonopen;
      //   this.websock.onerror = this.websocketonerror;
      //   this.websock.onclose = this.websocketclose;
      // },
      // websocketonopen(){ //连接建立之后执行send方法发送数据
      //   let actions = {
      //     data: this.sendmess,
      //     max_generation: this.inputValue1,
      //     population_size: this.inputValue2,
      //     p_mutation: this.inputValue,
      //   } ;  //发送markers
      //   this.websocketsend(JSON.stringify(actions));
      // },
      // websocketonerror(){//连接建立失败重连
      //   this.initWebSocket();
      // },
      // websocketonmessage(e){ //数据接收
      //   const redata = JSON.parse(e.data);
      // },
      // websocketsend(Data){//数据发送
      //   this.websock.send(Data);
      // },
      // websocketclose(e){  //关闭
      //   console.log('断开连接',e);
      // },
      }
    };
</script>