<template>
    <ejs-schedule height="600px" :selectedDate='schedulerSelectedDate' :eventSettings="appointmentData">
      <e-header-rows>
        <!-- <e-header-row option="Year"></e-header-row>       
      <e-header-row option="Month"></e-header-row>
      <e-header-row option="Week"></e-header-row>
      <e-header-row option="Date"></e-header-row>       
      <e-header-row option="Hour"></e-header-row>           -->
        <e-header-row option="Year" :template="'month-year-header'">
          <template v-slot:month-year-header="{data}">
            <span class="month-year-text">{{getMonthYearText(data)}}</span>
          </template>
        </e-header-row>
        <e-header-row option="Week" :template="'week-header'">
          <template v-slot:week-header="{data}">
            <span class="week-text">{{getWeekText(data)}}</span>
          </template>
        </e-header-row>
        <e-header-row option="Date"></e-header-row>
      </e-header-rows>
      <e-views>
         <!-- <e-view option='TimelineDay'></e-view>
        <e-view option='TimelineWeek'></e-view>
        <e-view option='TimelineWorkWeek'></e-view>  -->
        <e-view option="TimelineMonth" interval="12"></e-view>
      </e-views>
    </ejs-schedule>
</template>

<script> 
import { ScheduleComponent, ViewsDirective, ViewDirective, getWeekNumber, TimelineMonth, TimelineViews, HeaderRowsDirective, HeaderRowDirective } from "@syncfusion/ej2-vue-schedule";
import { Internationalization } from "@syncfusion/ej2-base";

var instance = new Internationalization();

export default {
  name: 'App',
  components: { 
    'ejs-schedule': ScheduleComponent,
    'e-header-rows': HeaderRowsDirective,
    'e-header-row': HeaderRowDirective,  
    'e-views' : ViewsDirective,
    'e-view'  : ViewDirective
  },
  provide : { schedule : [ TimelineViews, TimelineMonth ] },
  data() {
    return {
      schedulerSelectedDate : new Date(2022, 5, 7),
      appointmentData : {
         dataSource : [
             {
              Id : 1,
              Subject : 'Football',
              StartTime: new Date(2022, 5, 7, 9, 0, 0),
              EndTime: new Date(2022, 5, 7, 10, 0, 0)
            },
            {
              Id : 2,
              Subject : 'Hockey',
              StartTime: new Date(2022, 5, 9, 10, 0, 0),
              EndTime: new Date(2022, 5, 9, 11, 0, 0)
            }
         ]
      }
    };
  },
  methods : {
    getMonthYearText : function(value) {
      return instance.formatDate(value.date, { skeleton: 'yMMMM' });
    },
    getWeekText : function(value) {
      return 'Week' + ' ' + getWeekNumber(value.date);
    }

  }
}
</script>

<style>
  @import '../node_modules/@syncfusion/ej2-base/styles/material.css';
  @import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
  @import '../node_modules/@syncfusion/ej2-calendars/styles/material.css';
  @import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
  @import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
  @import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
  @import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
  @import '../node_modules/@syncfusion/ej2-vue-schedule/styles/material.css';
</style>
