import React, { useRef } from 'react';
import * as Highcharts from 'highcharts';
import HighchartsReact from 'highcharts-react-official';

let projectSummary = {
  totalSites: '1000',
  existingOnAirProjects: '200',
  locCoveredExistProj: '200',
  embActiveProjects: '200',
  locCoveredEmbActiveProj: '200',
  embNotActiveProjects: '300',
  locCoveredEmbNotActiveProj: '300',
  nbActiveProjects: '250',
  locCoveredNbActiveProj: '250',
  nbSmdbProjects: '37',
  locCoveredNbSmdbProj: '37',
  nbRawLandProjects: '13',
  locCoveredNbRawLandProj: '13',
};

let locationDetails = {
  existingOnAirProjUsableCap: '20',
  embActiveProjUsableCap: '20',
  embNotActiveProjUsableCap: '30',
  nbActiveProjUsableCap: '25',
  nbSmdbProjUsableCap: '3.7',
  nbRawLandProjUsableCap: '1.3',
};

let options = {
  chart: {
    type: 'pie',
    //width: 400,
    //height: 300,
    //height: (16 / 16) * 100 + "%",
    //marginTop: -200,
  },
  title: {
    text: 'Site Summary',
    style: {
      fontWeight: 'bold',
      fontSize: '12px',
      color: '#CD040B',
      fontFamily: '"nhg-display-bold", arial, sans-serif',
    },
    x: -10,
    y: 0,
  },
  subtitle: {
    text:
      'Total sites:' +
      Number(projectSummary?.totalSites).toLocaleString('en-US'),
    style: {
      fontSize: '10px',
      color: 'black',
    },
    x: -10,
    y: 20,
  },

  plotOptions: {
    allowPointSelect: true,
    cursor: 'pointer',
    pie: {
      //size: 200,
      startAngle: -90,
      endAngle: 90,
      center: ['50%', '75%'],
    },
    series: {
      dataLabels: {
        enabled: true,
        padding: 0,
        allowOverlap: true,
        crop: false,
        overflow: 'none',
        formatter: function () {
          if (this.y === 0) {
            return null;
          }
          return this.key + '<br>' + '<b>' + this.point.noOfSites + '</b>';
        },
      },
    },
  },
  tooltip: {
    formatter: function () {
      return (
        this.key +
        ': ' +
        '<b>' +
        this.point.noOfSites +
        '</b>' +
        '<br>' +
        'OFS: ' +
        '<b>' +
        this.point.locationsCovered +
        '</b>' +
        '<br>' +
        'Usable Cap: ' +
        '<b>' +
        this.point.usableCapacity +
        '</b>'
      );
    },
  },
  series: [
    {
      name: 'Sites',
      colorByPoint: true,
      size: '60%',
      innerSize: '70%',
      data: [
        {
          name: 'Existing On Air Sites',
          y:
            projectSummary.existingOnAirProjects /
            projectSummary.totalSites /
            100,
          //color: "#58508D",
          noOfSites: Number(
            projectSummary?.existingOnAirProjects
          )?.toLocaleString('en-US'),
          locationsCovered: Number(
            projectSummary?.locCoveredExistProj
          )?.toLocaleString('en-US'),
          usableCapacity: locationDetails?.existingOnAirProjUsableCap,
        },
        {
          name: 'Embedded Base - Active Project (Mod)',
          y: projectSummary.embActiveProjects / projectSummary.totalSites / 100,

          noOfSites: Number(projectSummary?.embActiveProjects)?.toLocaleString(
            'en-US'
          ),
          locationsCovered: Number(
            projectSummary?.locCoveredEmbActiveProj
          )?.toLocaleString('en-US'),
          usableCapacity: locationDetails?.embActiveProjUsableCap,

          color: 'rgb(92, 92, 97)',
        },
        {
          name: 'Embedded Base - No Active Project (Mod)',
          y:
            projectSummary.embNotActiveProjects /
            projectSummary.totalSites /
            100,

          noOfSites: Number(
            projectSummary?.embNotActiveProjects
          )?.toLocaleString('en-US'),
          locationsCovered: projectSummary?.locCoveredEmbNotActiveProj,
          usableCapacity: locationDetails?.embNotActiveProjUsableCap,
          color: 'rgb(255,188,117)',
        },
        {
          name: 'New Build - Active Project',
          y: projectSummary.nbActiveProjects / projectSummary.totalSites / 100,

          noOfSites: Number(projectSummary?.nbActiveProjects)?.toLocaleString(
            'en-US'
          ),
          locationsCovered: Number(
            projectSummary?.locCoveredNbActiveProj
          )?.toLocaleString('en-US'),
          usableCapacity: locationDetails?.nbActiveProjUsableCap,
          color: '#92B1B6',
        },

        {
          name: 'New Build - No Active Project (SMDB Existing Structure)',
          y: projectSummary.nbSmdbProjects / projectSummary.totalSites / 100,

          noOfSites: Number(projectSummary?.nbSmdbProjects)?.toLocaleString(
            'en-US'
          ),
          locationsCovered: Number(
            projectSummary?.locCoveredNbSmdbProj
          )?.toLocaleString('en-US'),
          usableCapacity: locationDetails?.nbSmdbProjUsableCap,
          color: 'rgb(153,158,255)',
        },
        {
          name: 'New Build - No Active Project (Raw Land)',
          y: projectSummary.nbRawLandProjects / projectSummary.totalSites / 100,
          color: 'rgb(153,158,255)',
          noOfSites: Number(projectSummary?.nbRawLandProjects)?.toLocaleString(
            'en-US'
          ),
          locationsCovered: Number(
            projectSummary?.locCoveredNbRawLandProj
          )?.toLocaleString('en-US'),
          usableCapacity: locationDetails?.nbRawLandProjUsableCap,
          color: 'rgb(241,92,128)',
        },
      ],
    },
  ],
  exporting: {
    buttons: {
      contextButton: {},
    },
  },
};

// const options: Highcharts.Options = {
//   title: {
//     text: 'My chart',
//   },
//   series: [
//     {
//       type: 'line',
//       data: [1, 2, 3],
//     },
//   ],
// };

// React supports function components as a simple way to write components that
// only contain a render method without any state (the App component in this
// example).

const App = (props: HighchartsReact.Props) => {
  const chartComponentRef = useRef(null);

  return (
    <HighchartsReact
      highcharts={Highcharts}
      options={options}
      ref={chartComponentRef}
      {...props}
    />
  );
};

export default App;
