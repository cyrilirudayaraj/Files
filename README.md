let options = {
    chart: {
      type: "pie",
      //width: 363,
      // height: 300,
      events: {
        drilldown: function (e) {
          this.axes.forEach((axis) =>
            axis.update({ visible: true }, false, false)
          );

          this.reflow();
          if (!e.seriesOptions) {
            if (e.point?.name === "OFS") {
              this.setTitle(null, {
                text:
                  "Total OFS:" +
                  Number(projectSummary?.totalLocCovered)?.toLocaleString(
                    "en-US"
                  ),
              });
              var chart = this,
                drilldowns1 = {
                  OFS: {
                    id: "OFS",
                    name: "Serving Cat",
                    type: "pie",
                    data: browserData,
                    size: "60%",
                    dataLabels: {
                      distance: "-30%",
                      padding: 0,
                      allowOverlap: true,
                      crop: false,
                      overflow: "none",
                      formatter: function () {
                        return this.point.name;
                      },
                      color: "black",
                      /// distance: -30,
                    },
                  },
                },
                drilldowns2 = {
                  OFS: {
                    id: "OFS",
                    name: "Cap/Non cap",
                    type: "pie",
                    data: versionsData,
                    size: "80%",
                    innerSize: "60%",
                    dataLabels: {
                      padding: 0,
                      allowOverlap: true,
                      crop: false,
                      overflow: "none",
                      formatter: function () {
                        // display only if larger than 1
                        console.log("test", this);
                        return (
                          "<b>" +
                          this.point.name +
                          ":</b> " +
                          this.point.servingStatus +
                          "(" +
                          this.y +
                          "%" +
                          ")"
                        );
                      },
                    },
                  },
                },
                series1 = drilldowns1[e.point.name],
                series2 = drilldowns2[e.point.name];

              chart.addSingleSeriesAsDrilldown(e.point, series1);
              chart.addSingleSeriesAsDrilldown(e.point, series2);
              chart.applyDrilldown();
            } else if (e.point?.name === "Uncovered") {
              this.setTitle(null, {
                text:
                  "Total Uncovered:" +
                  Number(projectSummary?.locationsUnCovered)?.toLocaleString(
                    "en-US"
                  ),
              });
              var chart = this,
                drilldowns1 = {
                  Uncovered: {
                    name: "Uncovered",
                    type: "pie",
                    data: browserDataUncoveredCategory,
                    size: "80%",
                    dataLabels: {
                      formatter: function () {
                        return (
                          "<b>" +
                          this.point.name +
                          ":</b> " +
                          this.point.servingStatus +
                          "(" +
                          this.y +
                          "%" +
                          ")"
                        );
                      },
                      color: "black",
                      //distance: -30,
                    },
                  },
                },
                series2 = drilldowns1[e.point.name];

              chart.addSingleSeriesAsDrilldown(e.point, series2);
              chart.applyDrilldown();
            }
          }
        },
        drillup: function (e) {
          this.setTitle(null, {
            text:
              "Total Locations:" +
              Number(projectSummary.totalLocations)?.toLocaleString("en-US") +
              "<br>" +
              "OFS: " +
              (
                (projectSummary.totalLocCovered /
                  projectSummary.totalLocations) *
                100
              )?.toFixed(2) +
              "%" +
              "<br>" +
              "Uncovered: " +
              (
                ((projectSummary.totalLocations -
                  projectSummary.totalLocCovered) /
                  projectSummary.totalLocations) *
                100
              )?.toFixed(2) +
              "%",
          });
          this.axes.forEach((axis) =>
            axis.update({ visible: false }, false, false)
          );

          this.reflow();
        },
      },
    },
    title: {
      text: "Location Serving Category Summary",
      style: {
        fontWeight: "bold",
        fontSize: "12px",
        color: "#CD040B",
        fontFamily: '"nhg-display-bold", arial, sans-serif',
      },
      x: -10,
      y: 20,
    },
    subtitle: {
      text:
        "Total Locations:" +
        Number(projectSummary.totalLocations)?.toLocaleString("en-US") +
        "<br>" +
        "OFS: " +
        (projectSummary.totalLocations > 0 ? (projectSummary.totalLocCovered / projectSummary.totalLocations) *
          100 : 0
        )?.toFixed(2) +
        "%" +
        "<br>" +
        "Uncovered: " +
        (
          projectSummary.totalLocations > 0 ? ((projectSummary.totalLocations - projectSummary.totalLocCovered) /
            projectSummary.totalLocations) *
            100 : 0
        )?.toFixed(2) +
        "%",
      style: {
        fontSize: "10px",
        color: "black",
      },
      x: -10,
      y: 40,
    },

    plotOptions: {
      allowPointSelect: true,
      cursor: "pointer",
      pie: {
        // size: 150,
      },
      series: {
        dataLabels: {
          enabled: true,
          padding: 0,
          allowOverlap: true,
          crop: false,
          overflow: "none",
          formatter: function () {
            if (this.y === 0) {
              return null;
            }
            if (this.key === "OFS" || this.key === "Uncovered") {
              return "<b>" + this.key + "</b><br>" + this.point.noOfLocations;
            } else {
              return this.point.noOfLocations;
            }
          },
        },
      },
    },
    tooltip: {
      formatter: function () {
        return "<b>" + this.point.toolTipName + ":</b> " + this.y + "%";
      },
    },

    series: [
      {
        name: "Locations",
        colorByPoint: true,
        size: "60%",
        data: [
          {
            name: "OFS",
            y: Number(
              (projectSummary.totalLocations > 0 ? (projectSummary.totalLocCovered /
                projectSummary.totalLocations) *
                100 : 0
              ).toFixed(2)
            ),
            noOfLocations: Number(
              projectSummary?.totalLocCovered
            )?.toLocaleString("en-US"),
            noOfSites: Number(projectSummary?.totalSites)?.toLocaleString(
              "en-US"
            ),
            color: "#FF6361",
            drilldown: true,
            toolTipName: "OFS",
          },
          {
            name: "Uncovered",

            y: Number(
              (projectSummary.totalLocations > 0 ? ((projectSummary.totalLocations -
                projectSummary.totalLocCovered) /
                projectSummary.totalLocations) *
                100 : 0
              ).toFixed(2)
            ),
            noOfLocations: Number(
              projectSummary.totalLocations - projectSummary.totalLocCovered
            )?.toLocaleString("en-US"),
            color: "#58508D",
            drilldown: true,
            toolTipName: "Uncovered",
          },
        ],
      },
    ],
  }
