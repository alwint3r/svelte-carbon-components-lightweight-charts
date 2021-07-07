<script>
  import {
    Column,
    Content,
    Grid,
    Row,
    SideNav,
    SideNavItems,
    SideNavLink,
  } from "carbon-components-svelte";
  import Header from "./components/Header.svelte";
  import Theme from "./components/Theme.svelte";
  import Chart from "svelte-lightweight-charts/components/chart.svelte";
  import LineSeries from "svelte-lightweight-charts/components/line-series.svelte";
  import { data } from "./data";
  import * as chartTheme from "./components/chart.theme";

  let theme = "g100";
  let isSideNavOpen = false;
  const usedChartTheme = theme === "g100" ? chartTheme.dark : chartTheme.light;

  const chartOptions = {
    height: 300,
    rightPriceScale: {
      borderVisible: false,
    },
    timeScale: {
      borderVisible: false,
    },
  };
</script>

<Theme persist bind:theme>
  <Header bind:isSideNavOpen />
  <SideNav bind:isOpen={isSideNavOpen}>
    <SideNavItems>
      <SideNavLink text="Dashboard" href="#/" />
      <SideNavLink text="Calibration" href="#/calibration" />
      <SideNavLink text="LoRaWAN Settings" href="#/lorawan-settings" />
      <SideNavLink text="Firmware Update" href="#/firmware-update" />
    </SideNavItems>
  </SideNav>
  <Content style="background: none; padding: 0.5rem; overflow: hidden">
    <Grid>
      <Row>
        <Column lg={16}>
          <h2 style="margin-bottom: 1.5rem">Dashboard</h2>
        </Column>
      </Row>
    </Grid>
    <Grid>
      <Row>
        <Column lg={6}>
          <Chart {...chartOptions} {...usedChartTheme.chart}>
            <LineSeries {data} {...usedChartTheme.lineSeries} />
            <LineSeries
              data={data.map((row) => ({ ...row, value: row.value - 10 }))}
              {...usedChartTheme.lineSeries}
              color="#FA4D56"
            />
          </Chart>
        </Column>
      </Row>
    </Grid>
  </Content>
</Theme>
