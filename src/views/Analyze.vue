<template>
    <div class="amap-page-container">
      <el-amap vid="amapDemo" :zoom="zoom" :center="center" class="amap-demo">
        <el-amap-marker vid="component-marker" :position="componentMarker.position" :content-render="componentMarker.contentRender" ></el-amap-marker>
        <el-amap-marker v-for="(marker, index) in markers" :position="marker.position" :events="marker.events" :visible="marker.visible" :draggable="marker.draggable" :vid="index" ></el-amap-marker>
      </el-amap>
      <div class="toolbar">
        <a-button type="primary" name="button" v-on:click="toggleVisible">toggle first marker</a-button>
        <a-button type="primary" name="button" v-on:click="changePosition">change position</a-button>
        <a-button type="primary" name="button" v-on:click="chnageDraggle">change draggle</a-button>
        <a-button type="primary" name="button" v-on:click="addMarker">add marker</a-button>
        <a-button type="primary" name="button" v-on:click="removeMarker">remove marker</a-button>
        <a-button type="primary" name="button" v-on:click="result">result</a-button>
      </div>
    </div>
</template>

  <style>
  .amap-page-container{
    height: 500px;
  }
  .toolbar{
    margin-top: 30px;
    text-align: center;
  }
  </style>

  <script>
    //import { AMapManager } from 'vue-amap';
    const exampleComponents = {
      props: ['text'],
      template: `<div>text from  parent: {{text}}</div>`
    }
    module.exports = {
      name: 'Analyze',
      data() {
        return {
          count: 1,
          slotStyle: {
            padding: '2px 8px',
            background: '#eee',
            color: '#333',
            border: '1px solid #aaa'
          },
          zoom: 14,
          center: [100.5273285, 38.21515044],
          markers: [
            {
              position: [100.5273285, 38.21515044],
              events: {
                click: () => {
                  alert('click marker');
                },
                dragend: (e) => {
                  console.log('---event---: dragend')
                  this.markers[0].position = [e.lnglat.lng, e.lnglat.lat];
                  this.$store.state.markers[0] = this.markers[0].position;
                }
              },
              visible: true,
              draggable: false,
              template: '<span>1</span>',
            }
          ],
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
      methods: {
        onClick(e) {
          this.count += 1;
          alert("555");
          console.log(amapManager.getMap());
          // let marker1 = {
          //   position: e.lnglat,
          // };
          // this.markers.push(marker1);
        },
        changePosition() {
          let position = this.markers[0].position;
          this.markers[0].position = [position[0] + 1, position[1] - 1];
          this.$store.state.markers[0] = this.markers[0].position;
        },
        chnageDraggle() {
          let draggable = this.markers[0].draggable;
          this.markers[0].draggable = !draggable;
          // console.log(this.markers[0].position);
        },
        toggleVisible() {
          let visableVar = this.markers[0].visible;
          this.markers[0].visible = !visableVar;
        },
        addMarker() {
          if(this.markers.length <= 25 )
          {
            let marker = {
            position: [100.5273285 + (Math.random() - 0.5) * 12, 38.21515044 + (Math.random() - 0.5) * 12]
          };
          this.markers.push(marker);
          this.$store.state.markers.push(marker.position);
          }
          else{
            this.$message.error('标点过量！！请不要超过25个');
          }
          
        },
        removeMarker() {
          if (!this.markers.length) return;
          this.markers.splice(this.markers.length - 1, 1);
          this.$store.markers.splice(this.markers.length - 1, 1);
        },
        result: function(){
	      this.$router.replace('/polyline');
	      this.way2 = 'result'
	}
      }
    };
</script>
