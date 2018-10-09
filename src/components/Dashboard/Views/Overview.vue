<template>
  <div>
    <!--Charts-->
    <div class="row">

      <div class="col-xs-12">
        <chart-card :chart-data="streamT" :chart-options="usersChart.options">
          <h4 class="title" slot="title">Temperatura ambiente: {{ (((temp*5000)/1023-500)/10).toFixed(1) }} ºC</h4>
          <span slot="subTitle"> </span>
          <span slot="footer">
            <i class="ti-reload"></i> Live Data </span>
          <div slot="legend">
            <i class="fa fa-circle text-info"></i> Sala I185 (Sala do Mini)
          </div>
        </chart-card>
      </div>

      <div class="col-md-6 col-xs-12">
        <chart-card :chart-data="preferencesChart.data"  chart-type="Pie">
          <h4 class="title" slot="title">Qualidade da Água</h4>
          <span slot="subTitle"> Castelo de Bode</span>
          <span slot="footer">
            <i class="ti-timer"></i> Última semana</span>
          <div slot="legend">
            <i class="fa fa-circle text-info"></i> Bom
            <i class="fa fa-circle text-warning"></i> Normal
            <i class="fa fa-circle text-danger"></i> Mau
          </div>
        </chart-card>
      </div>

      <div class="col-md-6 col-xs-12">
        <chart-card :chart-data="activityChart.data" :chart-options="activityChart.options">
          <h4 class="title" slot="title">Actividade dos Sensores</h4>
          <span slot="subTitle"> </span>
          <span slot="footer">
            <i class="ti-check"></i> Data information certified</span>
          <div slot="legend">
            <i class="fa fa-circle text-info"></i> Ox. dissolvido
            <i class="fa fa-circle text-warning"></i> pH
          </div>
        </chart-card>
      </div>

    </div>

  </div>
</template>
<script>

  import StatsCard from 'components/UIComponents/Cards/StatsCard.vue'
  import ChartCard from 'components/UIComponents/Cards/ChartCard.vue'
  import io from 'socket.io-client'

  export default {
    components: {
      StatsCard,
      ChartCard
    },

    methods: {
      coms () {
        setInterval(() => {
          var socket = io('http://localhost:3001')
          var vm = this
          socket.on('temp', function (msg) {
            vm.temp = parseInt(msg)
          // console.log(vm.temp)
          })
          vm.timer++
          vm.usersChart.data.series[0].push(((vm.temp * 5000) / 1023 - 500) / 10)
          vm.usersChart.data.series[0].shift()
          console.log(vm.usersChart.data)
        }, 1000)
      }
    },

    mounted () {
      this.coms()
    },
    computed: {
      streamT: function () {
        this.usersChart.data.labels.push(this.timer)
        this.usersChart.data.labels.shift()
        return this.usersChart.data
      }
    },
    /**
     * Chart data used to render stats, charts. Should be replaced with server data
     */

    data () {
      return {
        temp: 155,
        timer: 0,

        statsCards: [
          {
            type: 'warning',
            icon: 'ti-server',
            title: 'Capacity',
            value: '105GB',
            footerText: 'Updated now',
            footerIcon: 'ti-reload'
          },
          {
            type: 'success',
            icon: 'ti-wallet',
            title: 'Revenue',
            value: '$1,345',
            footerText: 'Last day',
            footerIcon: 'ti-calendar'
          },
          {
            type: 'danger',
            icon: 'ti-pulse',
            title: 'Errors',
            value: '23',
            footerText: 'In the last hour',
            footerIcon: 'ti-timer'
          },
          {
            type: 'info',
            icon: 'ti-twitter-alt',
            title: 'Followers',
            value: '+45',
            footerText: 'Updated now',
            footerIcon: 'ti-reload'
          }
        ],
        usersChart: {
          data: {
            labels: ['', '', '', '', '', '', '', ''],
            series: [
              [25, 25, 25, 25, 25, 25, 25, 25]
            ]
          },
          options: {
            low: 25,
            high: 32,
            showArea: true,
            height: '245px',
            axisX: {
              showGrid: false
            },
            showLine: true,
            showPoint: false
          }
        },
        activityChart: {
          data: {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'Mai', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            series: [
              [542, 543, 520, 680, 653, 753, 326, 434, 568, 610, 756, 895],
              [230, 293, 380, 480, 503, 553, 600, 664, 698, 710, 736, 798]
            ]
          },
          options: {
            seriesBarDistance: 10,
            axisX: {
              showGrid: false
            },
            height: '245px'
          }
        },
        preferencesChart: {
          data: {
            labels: ['62%', '32%', '6%'],
            series: [62, 32, 6]
          },
          options: {}
        }

      }
    }
  }

</script>
<style>

</style>
