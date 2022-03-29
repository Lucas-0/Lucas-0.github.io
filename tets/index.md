# 说是刷


<!--more-->


<div id="main" style="height: 30rem"></div>
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/echarts@5.3.1/dist/echarts.min.js"></script>
<script type="text/javascript">
var chartDom = document.getElementById('main');
var option;
option = {
  xAxis: {
    type: 'category',
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      data: [150, 230, 224, 218, 135, 147, 260],
      type: 'line'
    }
  ]
};
var myChart = echarts.init(chartDom, "dark" === document.body.getAttribute("theme") ? "dark" : "macarons");
option && myChart.setOption(option);
document.body.addEventListener('click', function(e) {
  if (e.target.className === 'fas fa-adjust fa-fw') {
    e.preventDefault();
    myChart.dispose();
    var themecolor = 'dark';
    themecolor = "dark" === document.body.getAttribute("theme") ? "dark": "macarons";
    myChart = echarts.init(document.getElementById('main'), themecolor);
    myChart.setOption(option);
  }
});
</script>
