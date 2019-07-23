<template>
  <div id="all">
<div id="getDate">
  <vuejs-datepicker v-model="StartDate" :value="this.default" :format="DatePickerFormat" ></vuejs-datepicker>
    <vuejs-datepicker v-model="EndDate" :format="DatePickerFormat"></vuejs-datepicker>
<p>
  {{ DateFormat(StartDate) }}
  {{ DateFormat(EndDate) }}
</p>
<p>{{ PeriodCalc() }}</p>
</div>
<div id="calendar">
  {{ Year }}
  {{ Month }}
  {{ Day }}
  <hr>
  <table border="0">
      <tr>
        <td id="headyear" v-for="year in Year">{{ year }}</td>
      </tr>
  </table>
  <table border="0">
      <tr>
        <td id="headmonth" v-for="month in Month">{{ month }}</td>
      </tr>
  </table>
  <table border="0">
      <tr>
        <td id="headday" v-for="day in Day">{{ day }}</td>
      </tr>
  </table>
  
  <table border="1" id="task">
    <th class="tag">No.</th>
    <th class="tag">タスク名</th>
    <th class="tag">開始日</th>
    <th class="tag">終了日</th>
    <th class="tag">達成率</th>
    <th class="tag">リソース</th>
    <th id="date">
      <table>
        <tr>
          <td class="date-info">
            s
          </td>
        <tr>
          <tr>
          <td class="date-info">
            d
          </td>
        <tr>
          <tr>
          <td class="date-info days">
            <li v-for="youbi in youbis">
              {{ youbi }}
            </li>
            </td>
        <tr>
          <tr>
          <td class="date-info days">
            <li v-for="days in Day">{{ days }}</li>
          </td>
        <tr>
          <tr>
          <td class="date-info">
            f
          </td>
        <tr>
      <table>
    </th>
  </table>
  
</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.10.6/moment.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.10.6/locale/ja.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script src="https://unpkg.com/vuejs-datepicker"></script>
</div>
</template>

<script>
  moment.locale('ja', {
    weekdays: ["日曜日","月曜日","火曜日","水曜日","木曜日","金曜日","土曜日"],
    weekdaysShort: ["日","月","火","水","木","金","土"],
});

var getDate = new Vue({
  el: '#getDate',
  data: {
    default:moment(),
    DatePickerFormat: 'yyyy/MM/dd',
    StartDate:'',
    EndDate:'',
    Period:0,
    MonthPeriod:0,
    YearPeriod:0,
    Year:[],
    Day:[],
    Daycount:[],
    Month:[],
    youbis:[]
  },
  methods:{
    DateFormat:function(date){
      return moment(date).format('YYYY/MM/DD')
    },
    MomentFormat:function(date){
      return moment(date)
    },
    PeriodCalc:function(stdate,endate){
      if(this.StartDate!=='' && this.EndDate!==''){
        console.log('Period Calc')
        this.Period = moment(this.EndDate).diff(moment(this.StartDate),'days')
        this.PeriodSet = true
        this.setYear()
        this.setMonth()
        this.setDate()
        writeCalendar.setYear(this.Year)
        writeCalendar.setMonth(this.Month)
        writeCalendar.setDate(this.Day,this.youbis)
        return this.Period
      }
    },
    setYear:function(){
      this.YearPeriod = moment(this.EndDate).diff(moment(this.StartDate),'year')
      for(var i=0;i<=this.YearPeriod;i++){
        this.Year[i] = moment(this.StartDate).add(i,'year').year()
      }
      console.log(this.Year)
      console.log(this.Year.length)
    },
    setMonth:function(){
      this.MonthPeriod = moment(this.EndDate).diff(moment(this.StartDate),'month')
      for(var i=0;i<=this.MonthPeriod;i++){
       this.Month[i] = moment(this.StartDate).add(i,'month').month() + 1
      }
      console.log(this.Month)
      console.log(this.Month.length)
    },
    
    setDate:function(){
      for(var i=0;i<=this.Period;i++){
       this.Day[i] = moment(this.StartDate).add(i,'days').date()
       this.youbis[i] = moment(moment(this.StartDate).add(i,'days')).format("ddd")
        console.log(this.youbis[i]+"曜日")
      }
      console.log(this.Day)
      console.log(this.Day.length)
      console.log(this.youbis)
      console.log(this.youbis.length)
    }
  },
  components: {
    vuejsDatepicker
  }
});

var writeCalendar = new Vue({
  el:'#calendar',
  data:{
    Year:[],
    Month:[],
    Day:[],
    youbis:[]
  },
  methods:{
    setYear:function(year){
      this.Year = year
      console.log('set')
    },
    setMonth:function(month){
      this.Month = month
      console.log('set')
    },
    setDate:function(day,youbi){
      this.Day = day
      console.log('set')
      //this.setCss()
      this.youbis = youbi
     },
  }
})
</script>

<style>
  
</style>
