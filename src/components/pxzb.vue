<template>
  <div id="pczb" style="height:100%;width:100%">
  </div>    
</template>

<script>
  import * as d3 from 'd3v4'

  export default {
    name: 'my_main',
    data () {
      return {
      }
    },
    methods:{
      drawpxzb(node)
      {          
        if (node.type.indexOf("HR")!=-1)
        {
          this.draw(this.$store.getters.getWeb_person["HR"])
        }
        else if (node.type.indexOf("finance")!=-1)
        {
          this.draw(this.$store.getters.getWeb_person["finance"])
        }
        else if (node.type.indexOf("Boss")!=-1)
        {
          this.draw(this.$store.getters.getWeb_person["Boss"])
        }
        else if (node.type.indexOf("development1")!=-1)
        {
          this.draw(this.$store.getters.getWeb_person["development1"])
        }
        else if (node.type.indexOf("development2")!=-1)
        {
          this.draw(this.$store.getters.getWeb_person["development2"])
        }
        else if (node.type.indexOf("development3")!=-1)
        {
          this.draw(this.$store.getters.getWeb_person["development3"])
        }
      },
      draw(data){
        console.log(data)
          var re=[]
          var _kinds=[]
          data.forEach(function(item){
            re.push([Number(item.day.slice(3,5)),item.hour,item.number,item.nature])
            _kinds.push(item.nature)
          })
          _kinds=Array.from(new Set(_kinds))

          console.log(re)

      var dom = document.getElementById("pczb");
       var myChart = this.$echarts.init(dom);
       var app = {};
       var option = null;

        var schema = [
        {name: 'Day', index: 0, text: 'Day'},
        {name: 'Hour', index: 1, text: 'Hour'},
        {name: 'Mounts', index: 2, text: 'Mounts'},
        {name: 'Kinds', index: 3, text: 'Kinds'}
        ];

        var lineStyle = {
          normal: {
            width: 1,
            opacity: 0.5
          }
        };

        option = {
          legend: {
            bottom: 30,
  /*          data: ['北京', '上海', '广州'],*/
            itemGap: 20,
            textStyle: {
              color: '#fff',
              fontSize: 14
            }
          },
          tooltip: {
            padding: 10,
            backgroundColor: '#222',
            borderColor: '#777',
            borderWidth: 1,
            formatter: function (obj) {
              var value = obj[0].value;
              return '<div style="border-bottom: 1px solid rgba(255,255,255,.3); font-size: 18px;padding-bottom: 7px;margin-bottom: 7px">'
              + obj[0].seriesName + ' ' + value[0] + '日期：'
              + value[3]
              + '</div>'
              + schema[1].text + '：' + value[1] + '<br>'
              + schema[2].text + '：' + value[2] + '<br>'
              + schema[3].text + '：' + value[3] + '<br>';
            }
          },
            // dataZoom: {
            //     show: true,
            //     orient: 'vertical',
            //     parallelAxisIndex: [0]
            // },
            parallelAxis: [
            {dim: 0, name: schema[0].text, inverse: true, max: 31, nameLocation: 'start'},
            {dim: 1, name: schema[1].text},
            {dim: 2, name: schema[2].text},
            {dim: 3, name: schema[3].text,type: 'category', data: _kinds}
              ],
                parallel: {
                  left: '18%',
                  right: '18%',
                  bottom: 100,
                  parallelAxisDefault: {
                    type: 'value',
                    name: 'AQI指数',
                    nameLocation: 'end',
                    nameGap: 20,
                    nameTextStyle: {
                      color: '#fff',
                      fontSize: 12
                    },
                    axisLine: {
                      lineStyle: {
                        color: '#aaa'
                      }
                    },
                    axisTick: {
                      lineStyle: {
                        color: '#777'
                      }
                    },
                    splitLine: {
                      show: false
                    },
                    axisLabel: {
                      textStyle: {
                        color: '#fff'
                      }
                    }
                  }
                },
                series:
                {
                  name: data[0].type,
                  type: 'parallel',
                  lineStyle: lineStyle,
                  data: re
                }
              };;
              if (option && typeof option === "object") {
                myChart.setOption(option, true);
              }

      }
    },
    mounted (){

    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>