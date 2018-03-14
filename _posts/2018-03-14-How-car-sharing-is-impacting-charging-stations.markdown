---
layout: post
title:  "The relevance of DriveNow's electric cars for Hamburg's charging infrastructure"
date:   2018-03-14 11:05:31
categories: eMobility
---

Casual observers of the public charging infrastructure in Hamburg will note that many of the spots are taken by car sharing companies -- specifically by [DriveNow and their i3s](https://www.drive-now.com/de/de/cars/bmw-i3). But **for how many charging transactions do they really account?** In short: **It's about a third**. This is based on 56 personal observations across the inner city of Hamburg. 

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

But how does that compare to the number of electric cars on the road? Turns out **DriveNow's i3s indeed have an outsized share of charging transactions** compared to all other electric cars on the road. Based on some extrapolation from data of the city of Hamburg there are ~2,800 EVs[^1] and PHEVs registered in Hamburg (this excludes electric cars that are not allowed on public roads). In comparison, there are only 200 electric DriveNows in Hamburg (as of Dec 2017).[^2] Let's assume that the number of non-local cars charging in Hamburg is roughly balanced by those that are registered in Hamburg but charge elsewhere. From that perspective **car sharing vehicles use about 4.3x as many charging transactions as you'd expect.** 

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
              2833/(2833+200)*100,	200/(2833+200)*100
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

Surely, you'll say that car sharing vehicles have -- on average -- higher mileage. And you'd be correct. The average car in Germany is driven ~14,000km each year.[^3] Statistics for car sharing vehicles are more difficult to come by. However, DriveNow claims their cars are utilized for 3-5h per day.[^4] Combine this with data from Berlin from 2015 that claims that the average trip takes 18min for 8km[^5] and you end up with 80-133km per day or 29,000-48,000km per year. On average, that's about  **~2.75x as many kilometers as private vehicles.** Assuming that EVs/PHEVs drive as much as regular cars (maybe a bit optimistic?), we can now (hopefully) compare apples to apples:

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
              (2833*14000)/((2833*14000)+(200*((29000+48000)/2)))*100,
              (200*((29000+48000)/2))/((2833*14000)+(200*((29000+48000)/2)))*100
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
                  max: 90,
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

While already closer, there is still quite a gap between observation and expectations: Adjusted for kilometers, **DriveNow vehicles still have 1.8x as many transactions at public charging stations than you'd expect**. So, what's left? Home charging, of course. DriveNow mostly relies on public charging stations with few exceptions where they recharge cars with mobile batteries in case of a deep discharge of a car. Regular owners, on the other hand, mostly charge at home. According to an US survey from 4 years ago **81% of all charging is done at home.**[^6] Only 10% of all charging is done at public charging stations with the remains taking place mostly at the workplace. I strongly suspect that the share of home charging is lower in Germany, but I couldn't find any data on this. Assuming that BMW's i3 has a roughly equivalent range to the average EV/PHEV on the road, we can try to approximate how home charging would influence the expected shares of public charging. Multiplying number of cars with average kilometers and share of public charging, we learn that **DriveNow's expected share would be 66% of all transactions at public charging stations**. Interestingly, that's almost twice what we observed. It seems regular EV owners are using public charging to a much larger extent that you'd expect. I can see the following factors being at play here:

- Surely, there are gaps in the data. My calculations are only based on 56 observations. Plus, we know little about the share of home charging in Germany. In many areas of Hamburg it is rare that people own a dedicated parking space
- Hamburg offers free parking while charging publicly. That's huge -- especially in the crowded inner city. DriveNow cars, on the other hand, can park anywhere for free
- DriveNow incentivizes people to park their cars at charging stations (30 free minutes). However, it takes quite a bit of time to find those stations and it's not that easy to actually charge the car if you don't do that regularly. So, how many people do really charge their car sharing vehicles?
- Public charging stations in Hamburg are cheap in comparison to many private offerings. Again, I believe if you were to ask Germans where they charge their cars, you would see a different share than in the US

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
              34,
              66
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
            text: 'Accounting for home-charging the picture flips'
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
Yes! Thanks to an agreement between the city of Hamburg and the two big car sharing providers (DriveNow and car2go), it is planned that **the number of electric car sharing vehicles will grow to 950 by the end of 2019**. This is on top to any deployments by smaller providers. If we assume that growth of the regular EV/PHEV fleet will continue at the current pace of 38% p.a., we'll see about 3,600 regular electric cars on the roads by Dec 2019. If that were the case, **charging stations could be used to ~60% by DriveNow and the likes** based on my actual observations. The share could be as high as 88% if you project based on home-charging ratios, etc.

### What did we learn?
- **Car sharing providers are already an important customer of the public charging infrastructure** and will become even more important in the future
- However, on average, **current utilization of the public infrastructure is [still very low](/emobility/2018/03/10/more-charging-points-in-hamburg-but-still-limited-uptake.html)** as I've shown in a separate post
- Hence, car sharing will be an important factor to **make charging stations more profitable** in the future
- **In some inner-city areas we may witness some shortage of chargers** which can be compensated by more chargers (already in the works) or higher prices (e.g., removing the free parking inventive)

The raw data of my personal collection can be found [here](/assets/2018-03-14-Users-of-Hamburgs-charging-infrastructure.csv).

[^1]: [Drucksache 21/10349](https://www.buergerschaft-hh.de/ParlDok/dokument/59190/haushaltsplan-2017-2018-einzelplan-7-0-%E2%80%9Ebeh%C3%B6rde-f%C3%BCr-wirtschaft-verkehr-und-innovation%E2%80%9C-hier-nachbewilligung-nach-%C2%A7-35-lho-und-stellungnahme.pdf), Buergerschaft der Freien und Hansestadt Hamburg, 12. Sep 2017

[^2]: [Automobilwoche, data from 2017](https://www.automobilwoche.de/article/20171205/AGENTURMELDUNGEN/312059989/carsharing-anbieter-erweitert-flotte-auf--bmw-i-drivenow-setzt-in-hamburg-verstaerkt-auf-elektroautos)

[^3]: [KBA, data from 2016](https://www.kba.de/DE/Statistik/Kraftverkehr/VerkehrKilometer/verkehr_in_kilometern_node.html)

[^4]: [Süddeutsche Zeitung, data from 2017](http://www.sueddeutsche.de/news/wirtschaft/auto---berlin-drivenow-mehr-kunden-mehr-autos-hoehere-auslastung-dpa.urn-newsml-dpa-com-20090101-180110-99-578734)

[^5]: [Tagesspiegel, data from 2015](https://www.tagesspiegel.de/berlin/neue-studie-zu-berlin-und-muenchen-carsharing-entlastet-den-verkehr-kaum/12461384.html)

[^6]: [InsideEVs, data from 2014](https://insideevs.com/most-electric-vehicle-owners-charge-at-home-in-other-news-the-sky-is-blue/)