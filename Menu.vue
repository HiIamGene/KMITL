  <template>
  <div id="chart">
  <b-navbar toggleable="lg" type="dark" variant="success">
      <b-navbar-brand  href="#">GrowX </b-navbar-brand>
      <b-collapse id="nav-collapse" is-nav>
        

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">

          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template slot="button-content"><em>User</em></template>
            <b-dropdown-item v-if="role === 'admin'" href='/#/register'>Register</b-dropdown-item>
            <b-dropdown-item href="/" @click="logout">Sign Out</b-dropdown-item>
            
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <b-button type="submit" @click="onHistory" variant="danger" style="width:200px;height:100px">Run graph</b-button><br><br>
    <!--<b-button type="botton" @click="onSetting" variant="danger" style="width:200px;height:100px">Setting</b-button>-->
    <h1 style="color:green;">Infomation</h1><hr>
  <font size="10" face="Courier New" >
  <table width="100%">
    <tr>

      <th>Photo</th><br>
      <img src="pic_trulli.jpg" width="500" height="333">

    </tr>

  </table>
  </font>
        <apexchart type=area height=350 :options="chartOptions" :series="series" />
      </div>
  </template>
  <script>
  import VueApexCharts from 'vue-apexcharts'
  import axios from 'axios'
  var light = null
  var humidity = null
  var temperature = null
  var quality = null
  var j = null
  var i = 0
  var farm = 1
  export default {
        components: {
          apexchart: VueApexCharts,
        },
        data(){
          return {
          
              records: [],
            series: [{
              name: 'Sensor light',
              data: [light.data[0], light.data[1], light.data[2], light.data[3], light.data[4], light.data[5], light.data[6]]
            }, {
              name: 'Sensor humidity',
              data: [humidity.data[0], humidity.data[1], humidity.data[2], humidity.data[3], humidity.data[4], humidity.data[5], humidity.data[6]]
            },{
              name: 'Sensor temperature',
              data: [temperature.data[0], temperature.data[1], temperature.data[2],temperature.data[3], temperature.data[4], temperature.data[5], temperature.data[6]]
            },{
              name: 'quality',
              data: [quality.data[0], quality.data[1], quality.data[2], quality.data[3], quality.data[4], quality.data[5], quality.data[6]]
            }],
            chartOptions: {
              dataLabels: {
                enabled: false
              },
              stroke: {
                curve: 'smooth'
              },


              xaxis: {
                type: 'datetime',
                categories: [light.str[0], light.str[1], light.str[2],
                  light.str[3], light.str[4], light.str[5],
                  light.str[6]
                ],
              },
              tooltip: {
                x: {
                  format: 'dd/MM/yy HH:mm'
                  
                },

              }
            }
          }
        },
        /*methods: {
          onHistory(evt) { 
            evt.preventDefault(), 
            axios.post('http://localhost:8000/sensors', {
                  farm_id: farm,
                  option: 'list'
                  }).then(res=>{
                    localStorage.setItem('usertoken',JSON.stringify(res)),
                    this.j=res.data.result.lenght
                    for (i=0,i<j,i++){
                      axios.post('http://localhost:8000/sensors', {
                      farm_id: farm,
                      option: 'list'
                      }).then(res=>{localStorage.setItem('usertoken',JSON.stringify(res))
                      if (res.data.result[i].type=='humidity') {
                        
                          axios.post('http://localhost:8000/sensor_logs', {
                          sen_id: this.str.data.result[i].sen_id ,
                          option: 'list'
                          }).then(res=>{localStorage.setItem('usertoken',JSON.stringify(res))
                          l=res.data.result.lenght
                          if (l<7){alert("info not enough")
                          break;}
                          else{
                            m=6
                            for(k=l-1,k>l-8,k--){humidity.data[m]=res.data.result[k].value
                            humidity.str[m]=res.data.result[k].time
                            m--}
                          }
                          }
                          )
                      }
                        else if (res.data.result[i].type=='light') {
                        
                          axios.post('http://localhost:8000/sensor_logs', {
                          sen_id: this.str.data.result[i].sen_id ,
                          option: 'list'
                          }).then(res=>{localStorage.setItem('usertoken',JSON.stringify(res))
                          l=res.data.result.lenght
                          if (l<7){alert("info not enough")
                          break;}
                          else{
                            m=6
                            for(k=l-1,k>l-8,k--){light.data[m]=res.data.result[k].value
                            light.str[m]=res.data.result[k].time
                            m--}

                      }
                      }) 
                      }else if(res.data.result[i].type=='temperature'){
                          axios.post('http://localhost:8000/sensor_logs', {
                          sen_id: this.str.data.result[i].sen_id ,
                          option: 'list'
                          }).then(res=>{localStorage.setItem('usertoken',JSON.stringify(res))
                          l=res.data.result.lenght
                          if (l<7){alert("info not enough")
                          break;}
                          else{
                            m=6
                            for(k=l-1,k>l-8,k--){temperature.data[m]=res.data.result[k].value
                            temperature.str[m]=res.data.result[k].time
                            m--
                            }
                            
                      }
                          }
                          )
                      } 
                      else {
                        axios.post('http://localhost:8000/sensor_logs', {
                          sen_id: this.str.data.result[i].sen_id ,
                          option: 'list'
                          }).then(res=>{localStorage.setItem('usertoken',JSON.stringify(res))
                          l=res.data.result.lenght
                          if (l<7){alert("info not enough")
                          break;}
                          else{
                            m=6
                            for(k=l-1,k>l-8,k--){quality.data[m]=res.data.result[k].value;
                            quality.str[m]=res.data.result[k].time}
                      }     m--
                          }
                      )

                        
                      }
                      }
                    )}
                  }

                    
          )}
           
  } */              
  }
  </script>
  <style>
  </style>
