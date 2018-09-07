# 基于jq自更新年月组件jquery.daterangepicker.js

### 第一步，引入依赖：

   <script src="jquery.daterangepicker.js"></script>  
   `<link rel="stylesheet" href="daterangepicker.css">`

### 第二步，html部分  
   
   `<input id="dateTimeRange" value="" type="text" style="text-align:center;"> `
   

### 第三部，js部分

 单年月使用：
 
 ` $("#dateTimeRange").dateRangePicker({                               
                autoClose: true,
                singleDate: true,
                showShortcuts: false,
                language: 'cn',
                startOfWeek: 'monday',
            });
  `
  

双年月：

$("#dateTimeRange").dateRangePicker({ 

                autoClose: true, 
                
                separator: ' 至 ', 
                
                language: 'auto', 
                
                // startOfWeek: 'monday', 
                
                shortcuts: null,
                
                customShortcuts: [
                    {
                        name: '上周, ',
                        dates: function () {
                            if (_year == 0) {
                                let start = moment().weekday((-7 + (7 * _week))).toDate();
                                let end = moment().weekday((-1 + (7 * _week))).toDate();
                                return [start, end];
                            } else {
                                let start = new Date(_year, _mouth - 1, _day);
                                let end = new Date(_year, _mouth - 1, _day - 6);
                                return [start, end];
                            }

                        }
                    },
                    {
                        name: '本周, ',
                        dates: function () {
                            _week = 0;
                            //设置本周日期
                            let start = moment().weekday(0).toDate();
                            let end = moment().weekday(6).toDate();
                            return [start, end];
                        }
                    },
                    {
                        name: '下周',
                        dates: function () {
                            if (_year == 0) {
                                let start = moment().weekday(7 + 7 * _week).toDate();
                                let end = moment().weekday(13 + 7 * _week).toDate();
                                return [start, end];
                            } else {
                                let start = new Date(_year1, _mouth1 - 1, _day1 + 8);
                                let end = new Date(_year1, _mouth1 - 1, _day1 + 14);
                                return [start, end];
                            }
                        }
                    },
                    {
                        name: '上月, ',
                        dates: function () {
                            if (_year == 0) {
                                let currentTime = new Date();
                                let minDate = new Date(currentTime.getFullYear(), currentTime.getMonth() - 1 + _mouth, +1);
                                let maxDate = new Date(currentTime.getFullYear(), currentTime.getMonth() + 0 + _mouth, +0);
                                return [minDate, maxDate];
                            } else {
                                //console.log(_minM);
                                let start = new Date(_year, _minM - 1, 1);
                                let end = new Date(_year, _minM, 0);
                                return [start, end];
                            }

                        }
                    },
                    {
                        name: '本月, ',
                        dates: function () {
                            //设置当月日期
                            let currentTime = new Date();
                            let minDate = new Date(currentTime.getFullYear(), currentTime.getMonth(), +1);
                            let maxDate = new Date(currentTime.getFullYear(), currentTime.getMonth() + 1, +0);
                            return [minDate, maxDate];
                        }
                    },
                    {
                        name: '下月',
                        dates: function () {
                            if (_year == 0) {
                                let currentTime = new Date();
                                let minDate = new Date(currentTime.getFullYear(), currentTime.getMonth() + 1 + _mouth, +1);
                                let maxDate = new Date(currentTime.getFullYear(), currentTime.getMonth() + 2 + _mouth, +0);
                                return [minDate, maxDate];
                            } else {
                                let start = new Date(_year1, _maxM + 1, 1);
                                let end = new Date(_year1, _maxM + 2, 0);
                                return [start, end];
                            }

                        }
                    }
                ],
            }).bind('datepicker-change', function (event, obj) {
              //这里更改时间后触发的事件
            });

        }
        获取选择到的值：$("#dateTimeRange").val(); 

