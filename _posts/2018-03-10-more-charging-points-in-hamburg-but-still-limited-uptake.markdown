---
layout: post
title:  "Hamburg is investing strongly into their charging infrastructure, but daily usage remains limited"
date:   2018-03-10 11:05:31
categories: eMobility
---

Hamburg is very much at the forefront of e-Mobility in Germany -- in parts thanks to an ambitious government-driven “masterplan” for charging stations. Until the end of 2017 Hamburg deployed more than 600 public charging points at 300 locations throughout the city. An additional 400 charging points are expected to be online until 2019. The goal is to break the catch-22 situation of people avoiding the purchase of electric cars due to the limited charging infrastructure.[^1]

Thanks to a recent [public presentation](https://www.now-gmbh.de/content/1-aktuelles/1-presse/20180226-fachkonf-bundesfoerderung-bringt-elektromobilitaet-entscheidend-voran/tag-2_2-2-2_zisler-hamburg.pdf) of a representative of Stromnetz Hamburg, the company in charge of building the infrastructure, we now have a much better picture of the public uptake (see the chart below). As you can see, Hamburg has indeed been busy deploying new charging stations at a steady pace. From mid 2016 until mid 2017 the number of public stations grew by more than 50%. This compares to a 36% growth in electric cars in Hamburg within the same time frame.[^2]

Not surprisingly considering these two figures, the number of daily transactions per station remained largely flat with some fluctuation that might be explained by seasonality effects (e.g., increased usage of electric DriveNow cars during winter, higher battery consumption in the cold, ...). Similarly, kilowatt hours per transaction stayed roughly flat fluctuating between 9 and 12 kWh.

Striking are the low absolute numbers. At just ~1 daily transaction per station, most stations seem to be heavily underutilized. However, it is important to note that there seems to be a high variability across stations. As remarked in a recently published report of the local government[^2], some locations see as many as 8 transactions per day.

While it would be nice to see a bigger uptake of the public charging infrastructure, it is great to see that the city of Hamburg is willing to invest for the long-term. More so, it is commendable that Hamburg decided to not just focus on the sweet spots in the city center but to also build locations outside the center. This should greatly help to make the case to the public that Hamburg is ready for the growth in e-Mobility.

<div class="chart-container" style="position: relative; min-height:400px">
<canvas id="chargingChart1"></canvas>
</div>
<script>
  window.chartColors = {
    red: 'rgb(255, 99, 132)',
    orange: 'rgb(255, 159, 64)',
    yellow: 'rgb(255, 205, 86)',
    green: 'rgb(75, 192, 192)',
    blue: 'rgb(54, 162, 235)',
    purple: 'rgb(153, 102, 255)',
    grey: 'rgb(201, 203, 207)'
  };
  var ctx = document.getElementById("chargingChart1").getContext('2d');
  Chart.defaults.global.defaultFontSize = 16;
  Chart.defaults.global.defaultFontColor = '#111';
  Chart.defaults.global.maintainAspectRatio = false;
  var chargingChart1 = new Chart(ctx, {
      type: 'line',
      data: {
          labels: ["Jul 16",	"Aug 16",	"Sep 16",	"Oct 16",	"Nov 16",	"Dec 16",	"Jan 17",	"Feb 17",	"Mar 17",	"Apr 17",	"May 17",	"Jun 17",	"Jul 17",	"Aug 17",	"Sep 17",	"Oct 17",	"Nov 17",	"Dec 17",	"Jan 18"],

          datasets: [{
            label: 'Charging locations (Stromnetz Hamburg)',
            borderColor: window.chartColors.blue,
            backgroundColor: window.chartColors.blue,
            fill: false,
            data: [
              108,	114,	123,	132,	134,	138,	146,	148,	160,	180,	197,	206,	220,	249,	274,	297,	309,	311,	324
            ],
            yAxisID: 'y-axis-1',
          }, {
            label: 'Transactions / location / day',
            borderColor: window.chartColors.red,
            backgroundColor: window.chartColors.red,
            fill: false,
            data: [
              0.9,	0.78,	0.83,	0.8,	0.93,	0.98,	0.97,	0.95,	0.91,	0.82,	0.79,	0.73,	0.67,	0.68,	0.7,	0.74,	0.87,	0.96,	1.06
            ],
            yAxisID: 'y-axis-2'
          }]

      },
      options: {
          responsive: true,
          hoverMode: 'index',
          stacked: false,
          title: {
            display: true,
            text: 'Transactions at the public charging points in Hamburg'
          },
          scales: {
              yAxes: [{
                type: 'linear', 
                display: true,
                position: 'left',
                ticks: {
                  beginAtZero: true
                },
              	scaleLabel: {
                	display: true,
                  labelString: 'Locations'
                },
                id: 'y-axis-1'
              }, {
                type: 'linear', 
                beginAtZero: true,
                display: true,
                position: 'right',
                ticks: {
                  beginAtZero: true
                },
              	scaleLabel: {
                	display: true,
                  labelString: 'Transactions / location / day'
                },
                id: 'y-axis-2',

                gridLines: {
                  drawOnChartArea: false
                },
              }],
            }

      }
  });
</script>

_Source: Stromnetz Hamburg[^1]_

[^1]: Ladeinfrastruktur und Netzintegration, 5. Fachkonferenz Elektromobilität vor Ort, 27. Feb 2018 Leipzig

[^2]: Drucksache 21/10349, Buergerschaft der Freien und Hansestadt Hamburg, 12. Sep 2017