<script setup  lang="ts">

import * as d3 from 'd3';
import { onMounted } from 'vue';

const div = d3.selectAll('div');

onMounted(() => {
  const marge = { top: 10, bottom: 60, left: 10, right: 60 };
  const dataset = [2.5, 2.1, 1.7, 1.3, 0.9];
  const scaleLinear = d3
    .scaleLinear()
    .domain([0, d3.max(dataset)])
    .range([0, 250]);
  const svg = d3.select('svg');
  const g = svg.append('g').attr('transform', 'translate(' + marge.top + ',' + marge.left + ')');
  const rectHeight = 30;
  g.selectAll('rect')
    .data(dataset)
    .enter()
    .append('rect')
    .attr('x', 20)
    .attr('y', function (d: any, i: number) {
      return i * rectHeight;
    })
    .attr('width', function (d: any) {
      return scaleLinear(d);
    })
    .attr('height', rectHeight - 5)
    .attr('fill', 'lightblue');
  const xScale = d3
    .scaleLinear()
    .domain([0, d3.max(dataset)])
    .range([0, 250]);
  const xAxis = d3.axisBottom(xScale).ticks(7);
  g.append('g')
    .attr('transform', 'translate(' + 20 + ',' + dataset.length * rectHeight + ')')
    .call(xAxis);
});
</script>

<template>
  <div>
    <h2>Axis</h2>
    <svg width="960" height="600"></svg>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
