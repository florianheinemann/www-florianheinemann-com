---
layout: post
title:  "Hamburg investiert in mehr Ladepunkte. Die Nutzung bleibt aber weiterhin auf niedrigem Niveau"
date:   2018-03-10 11:05:32
categories: eMobility
---

Hamburg hat sich in den letzten Jahren als Vorreiter in Sachen Elektromobilität in Deutschland positioniert. Dies ist unter Anderem dem _Masterplan Ladeinfrastruktur_ zu verdanken der zur Installation von mehr als 600 öffentlichen Ladepunkten an 300 Standorten bis Ende 2017 geführt hat. Weitere 400 Ladepunkte sind bereits bis 2019 eingeplant. Damit soll auch das Henne-Ei Problem gelöst werden, dass potentielle Käufer von Elektroautos weiterhin vom Kauf zurückschrecken wegen mangelnder Infrastruktur.[^1]

Dank einer [öffentlichen Präsentation](https://www.now-gmbh.de/content/1-aktuelles/1-presse/20180226-fachkonf-bundesfoerderung-bringt-elektromobilitaet-entscheidend-voran/tag-2_2-2-2_zisler-hamburg.pdf) von Stromnetz Hamburg, der Betreiber der öffentlichen Ladeinfrastruktur, haben wir jetzt auch ein deutlich besseres Bild davon wie intensiv die Ladepunkte denn wirklich genutzt werden (siehe unten). Wie auf der Grafik sichtbar hat sich die Anzahl der öffentlichen Ladepunkte in der Tat drastisch erhöht. Allein zwischen Mitte 2016 und Mitte 2017 ist die Anzahl um mehr als 50% gewachsen und damit sogar schneller als die Anzahl an Elektroautos in Hamburg (36%).[^2]

Nicht überraschend bei diesen Zahlen ist die Anzahl der Ladevorgänge pro Station relativ flach geblieben, wenn man von den Saisoneffekten absieht (höhere Nutzung der Car Sharing Fahrzeuge im Winter, höherer Batterieverbrauch im Winter, etc.) Auch die durchschnittliche Lademenge ist mit 9-12 kWh recht konstant geblieben.

Überraschend ist wie gering die absoluten Zahlen sind. Mit rund einem Ladevorgang pro Tag bleiben die meisten Standorte weiterhin unterausgelastet. Es muss allerdings erwähnt werden, dass das Nutzungsverhalten über die Stationen hinweg sehr unterschiedlich zu sein scheint. Manche Stationen werden wohl bis zu 8 mal am Tag genutzt.[^2]

Auch wenn man sich eine breitere Nutzung der Stationen wünschen würde, ist es doch erfreuend zu sehen, dass die Stadt Hamburg bereit ist langfristig zu investieren. Dass die Stadt sich auch auf weniger genutzte Standorte außerhalb des Zentrums konzentriert, wird sicherlich über die nächsten Jahre die Akzeptanz der Elektromobilität weiter erhöhen.

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
            label: 'Ladestandorte (Stromnetz Hamburg)',
            borderColor: window.chartColors.blue,
            backgroundColor: window.chartColors.blue,
            fill: false,
            data: [
              108,	114,	123,	132,	134,	138,	146,	148,	160,	180,	197,	206,	220,	249,	274,	297,	309,	311,	324
            ],
            yAxisID: 'y-axis-1',
          }, {
            label: 'Ladevorgänge / Standort / Tag',
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
            text: 'Ladevorgänge an den öffentlichen Ladesäulen in Hamburg'
          },
          scales: {
              yAxes: [{
                type: 'linear', 
                display: true,
                position: 'left',
                ticks: {
                  beginAtZero: true
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
                id: 'y-axis-2',

                gridLines: {
                  drawOnChartArea: false
                },
              }],
            }

      }
  });
</script>

Quelle: Stromnetz Hamburg[^1]

[^1]: Ladeinfrastruktur und Netzintegration, 5. Fachkonferenz Elektromobilität vor Ort, 27. Feb 2018 Leipzig

[^2]: Drucksache 21/10349, Buergerschaft der Freien und Hansestadt Hamburg, 12. Sep 2017