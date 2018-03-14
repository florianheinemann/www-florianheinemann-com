---
layout: post
title:  "The relevance of DriveNow's electric cars for Hamburg's charging infrastructure"
date:   2018-03-14 11:05:31
categories: eMobility
---

Casual observers of the public charging infrastructure in Hamburg will note that many of the spots are taken by car sharing companies -- specifically by [DriveNow and their i3s](https://www.drive-now.com/de/de/cars/bmw-i3). But **for how many cars do they really account?** In short: **It's about a third**. This is based on 56 personal observations across the inner city of Hamburg. 

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
      type: 'bar',
      data: {
          labels: ['Local (HH)', 'DriveNow', 'Non-local', 'Other private*'],
          datasets: [{
            label: 'Share of observed charging transactions',
            borderColor: window.chartColors.blue,
            backgroundColor: window.chartColors.blue,
            fill: false,
            data: [
              25/0.56, 16/0.56, 11/0.56, 4/0.56
            ],
            yAxisID: 'y-axis-1',
          }]

      },
      options: {
            tooltips: {
                callbacks: {
                    label: function(tooltipItem, data) {
                        return Math.round(tooltipItem.yLabel*10)/10+'%';
                    }
                }
            },
          responsive: true,
          hoverMode: 'index',
          stacked: false,
          title: {
            display: true,
            text: 'DriveNow accounts for ~30% of all public charging (n=56)'
          },
          scales: {
          		xAxes: [ {
              	scaleLabel: {
                	display: true,
                  labelString: 'License plates'
                }
              }],
              yAxes: [{
                type: 'linear', 
                display: true,
                position: 'left',
                ticks: {
                  min: 0,
                  max: 50,
                  callback: function(value) {
                  	return value + "%"
                  }
                },
                id: 'y-axis-1'
              }],
            }
      }
  });
</script>

_Source: Personal data collection in early March 2018. Focus on inner city ranging from Eimsbüttel in the West, Winterhude in the North, Wandsbek in the East, and HafenCity in the South. (*): Includes leasing cars such as the ones of Yellow Strom_

But how does that compare to the number of electric cars on the road? Turns out **DriveNow's i3s indeed have an outsized share of charging transactions** compared to all other electric cars on the road. According to the city of Hamburg there are 2,205 EVs and PHEVs registered in Hamburg (this excludes electric cars that are not allowed on public roads). In comparison, there are only 70 electric DriveNows in Hamburg (as of June 2017).[^1] Let's assume that the number of non-local cars charging in Hamburg is roughly balanced by those that are registered in Hamburg but charge elsewhere. From that perspective **car sharing vehicles use about 9x as many charging transactions as you'd expect.** 

<div class="chart-container" style="position: relative; min-height:400px">
<canvas id="chargingChart2"></canvas>
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
  var ctx = document.getElementById("chargingChart2").getContext('2d');
  Chart.defaults.global.defaultFontSize = 16;
  Chart.defaults.global.defaultFontColor = '#111';
  Chart.defaults.global.maintainAspectRatio = false;
  var chargingChart2 = new Chart(ctx, {
      type: 'bar',
      data: {
          labels: ["Regular EVs/PHEVs",	"DriveNow's i3s"],

          datasets: [{
            label: 'Share of charging transactions',
            borderColor: window.chartColors.blue,
            backgroundColor: window.chartColors.blue,
            fill: false,
            data: [
              (56-16)/56*100, 16/56*100
            ]
          }, {
            label: 'Share of cars',
            borderColor: window.chartColors.red,
            backgroundColor: window.chartColors.red,
            fill: false,
            data: [
              2205/(2205+70)*100,	70/(2205+70)*100
            ]
          }]

      },
      options: {
            tooltips: {
                callbacks: {
                    label: function(tooltipItem, data) {
                        return Math.round(tooltipItem.yLabel*10)/10+'%';
                    }
                }
            },
          responsive: true,
          hoverMode: 'index',
          stacked: false,
          title: {
            display: true,
            text: 'DriveNow has an outsized share of charging transactions'
          },
          scales: {
              yAxes: [{
                type: 'linear', 
                display: true,
                position: 'left',
                ticks: {
                  min: 0,
                  max: 100,
                  callback: function(value) {
                  	return value + "%"
                  }
                },
                id: 'y-axis-1'
              }],
            }

      }
  });
</script>

_Source: Personal data collection and data of the city of Hamburg[^1]_

Surely, you'll say that car sharing vehicles have -- on average -- higher mileage. And you'd be correct. The average car in Germany is driven ~14,000km each year.[^2] Statistics for car sharing vehicles are more difficult to come by. However, DriveNow claims their cars are utilized for 3-5h per day.[^3] Combine this with data from Berlin from 2015 that claims that the average trip takes 18min for 8km[^4] and you end up with 80-133km per day or 29,000-48,000km per year. On average, that's about  **~2.75x as many kilometers as private vehicles.** Assuming that EVs/PHEVs drive as much as regular cars (maybe a bit optimistic?), we can now compare apples to apples:

<div class="chart-container" style="position: relative; min-height:400px">
<canvas id="chargingChart3"></canvas>
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
  var ctx = document.getElementById("chargingChart3").getContext('2d');
  Chart.defaults.global.defaultFontSize = 16;
  Chart.defaults.global.defaultFontColor = '#111';
  Chart.defaults.global.maintainAspectRatio = false;
  var chargingChart3 = new Chart(ctx, {
      type: 'bar',
      data: {
          labels: ["Regular EVs/PHEVs",	"DriveNow's i3s"],

          datasets: [{
            label: 'Share of charging transactions',
            borderColor: window.chartColors.blue,
            backgroundColor: window.chartColors.blue,
            fill: false,
            data: [
              (56-16)/56*100, 16/56*100
            ]
          }, {
            label: 'Share of driven kilometers',
            borderColor: window.chartColors.red,
            backgroundColor: window.chartColors.red,
            fill: false,
            data: [
              (2205*14000)/((2205*14000)+(70*((29000+48000)/2)))*100,
              (70*((29000+48000)/2))/((2205*14000)+(70*((29000+48000)/2)))*100
            ]
          }]

      },
      options: {
            tooltips: {
                callbacks: {
                    label: function(tooltipItem, data) {
                        return Math.round(tooltipItem.yLabel*10)/10+'%';
                    }
                }
            },
          responsive: true,
          hoverMode: 'index',
          stacked: false,
          title: {
            display: true,
            text: 'Adjusted for km DriveNow still has an outsized share of transactions'
          },
          scales: {
              yAxes: [{
                type: 'linear', 
                display: true,
                position: 'left',
                ticks: {
                  min: 0,
                  max: 100,
                  callback: function(value) {
                  	return value + "%"
                  }
                },
                id: 'y-axis-1'
              }],
            }

      }
  });
</script>

_Source: Personal data collection and data of the city of Hamburg[^1]_

The picture remains largely unchanged: Adjusted for kilometers, **DriveNow vehicles still have 3.6x as many transactions at public charging stations than you'd expect**. So, what's left? Home charging, of course. DriveNow mostly relies on public charging stations with few exceptions where they recharge cars with mobile batteries in case of a deep discharge of a car. Regular owners, on the other hand, mostly charge at home. According to an US survey from 4 years ago **81% of all charging is done at home.**[^5] Or saying it differently, only one fifth of all charging is done at public charging stations or elsewhere (e.g., at the workplace). Assuming that BMW's i3 has a roughly equivalent range to the average EV/PHEV on the road, we can try to approximate how home charging would influence the expected shares of public charging. Multiplying number of cars with average kilometers and share of public charging, we learn that **DriveNow's expected share would be 30% of all transactions at public charging stations**. Interestingly, that's almost exactly equal to the observed share of transactions. 

Of course, this is just a very rough approximation of what's happening. It does, for example, not account for the incentive (in the form of free minutes) that DriveNow customers receive to recharge their car. It does also ignore the different costs of charging at home vs. charging at a public station, etc. 

<div class="chart-container" style="position: relative; min-height:400px">
<canvas id="chargingChart4"></canvas>
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
  var ctx = document.getElementById("chargingChart4").getContext('2d');
  Chart.defaults.global.defaultFontSize = 16;
  Chart.defaults.global.defaultFontColor = '#111';
  Chart.defaults.global.maintainAspectRatio = false;
  var chargingChart4 = new Chart(ctx, {
      type: 'bar',
      data: {
          labels: ["Regular EVs/PHEVs",	"DriveNow's i3s"],

          datasets: [{
            label: 'Observed share of charging transactions',
            borderColor: window.chartColors.blue,
            backgroundColor: window.chartColors.blue,
            fill: false,
            data: [
              (56-16)/56*100, 16/56*100
            ]
          }, {
            label: 'Expected share',
            borderColor: window.chartColors.red,
            backgroundColor: window.chartColors.red,
            fill: false,
            data: [
              69.9,
              30.4
            ]
          }]

      },
      options: {
            tooltips: {
                callbacks: {
                    label: function(tooltipItem, data) {
                        return Math.round(tooltipItem.yLabel*10)/10+'%';
                    }
                }
            },
          responsive: true,
          hoverMode: 'index',
          stacked: false,
          title: {
            display: true,
            text: 'Accounting for home-charging the situation balances out'
          },
          scales: {
              yAxes: [{
                type: 'linear', 
                display: true,
                position: 'left',
                ticks: {
                  min: 0,
                  max: 80,
                  callback: function(value) {
                  	return value + "%"
                  }
                },
                id: 'y-axis-1'
              }],
            }

      }
  });
</script>

_Source: Personal data collection and data of the city of Hamburg[^1]_

### Any implications for the future?
Yes! Thanks to an agreement between the city of Hamburg and the two big car sharing providers (DriveNow and car2go), it is planned that **the number of electric car sharing vehicles will grow to 950 by the end of 2019**. This is on top to any deployments by smaller providers. If we assume that growth of the regular EV/PHEV fleet will continue at the current pace of 38% p.a., we'll see about 3,600 regular electric cars on the roads by Dec 2019. If that were the case, **charging stations would be used to almost 80% by DriveNow and the likes**.

### What did we learn?
- **Car sharing providers are already an important customer of the public charging infrastructure** and will become even more important in the future
- However, on average, **current utilization is [still very low](/emobility/2018/03/10/more-charging-points-in-hamburg-but-still-limited-uptake.html)** as I've shown in a separate post
- Hence, car sharing will be an important factor to **make charging stations more profitable** in the future
- **In some inner-city areas we may witness some shortage of chargers** which can be compensated by more chargers (already in the works) or higher prices (e.g., removing the free parking inventive)

The raw data of my personal collection can be found [here](/assets/2018-03-14-Users-of-Hamburgs-charging-infrastructure.csv).

[^1]: [Drucksache 21/10349](https://www.buergerschaft-hh.de/ParlDok/dokument/59190/haushaltsplan-2017-2018-einzelplan-7-0-%E2%80%9Ebeh%C3%B6rde-f%C3%BCr-wirtschaft-verkehr-und-innovation%E2%80%9C-hier-nachbewilligung-nach-%C2%A7-35-lho-und-stellungnahme.pdf), Buergerschaft der Freien und Hansestadt Hamburg, 12. Sep 2017

[^2]: [KBA, data from 2016](https://www.kba.de/DE/Statistik/Kraftverkehr/VerkehrKilometer/verkehr_in_kilometern_node.html)

[^3]: [Süddeutsche Zeitung, data from 2017](http://www.sueddeutsche.de/news/wirtschaft/auto---berlin-drivenow-mehr-kunden-mehr-autos-hoehere-auslastung-dpa.urn-newsml-dpa-com-20090101-180110-99-578734)

[^4]: [Tagesspiegel, data from 2015](https://www.tagesspiegel.de/berlin/neue-studie-zu-berlin-und-muenchen-carsharing-entlastet-den-verkehr-kaum/12461384.html)

[^5]: [InsideEVs, data from 2014](https://insideevs.com/most-electric-vehicle-owners-charge-at-home-in-other-news-the-sky-is-blue/)