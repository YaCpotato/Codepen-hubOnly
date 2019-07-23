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
  
</script>
