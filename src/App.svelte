
<main>
  <div class="outer-wrapper">  
    <div id="pizza-container">
    </div>
  </div>
</main>

<script>
  import {pie, arc} from 'd3-shape'
  import {select, selectAll} from 'd3-selection'
  import {onMount} from 'svelte';

  let width = window.innerWidth
  let height = window.innerHeight
  console.log(width,height)
  let margin = {top: 10, right: 10, bottom: 10, left:10}
  let radius = (Math.min(width, height) / 2) * 0.8

  onMount(() => {

    let svg = select('#pizza-container')
    .append("svg")
      .attr("width", width)
      .attr("height", height)
    .append("g")
      .attr("transform", "translate(" + width / 2 + "," + height / 2 + ")")

    const data = [
      {"size":10, "topping":2},
      {"size":8, "topping":3},
      {"size":5, "topping":3},
      {"size":10, "topping":3},
      {"size":12, "topping":3},
      {"size":6, "topping":3},
      {"size":8, "topping":3},
      {"size":8, "topping":3},
      {"size":8, "topping":3}
    ]
    const arcs = pie().value(d => d.size)(data);
    const arced = arc()
        .innerRadius(0)
        .outerRadius(radius);

    console.log(arcs)
    svg
      .selectAll('.slices')
      .data(arcs)
      .enter()
      .append('path')
      .attr('d', arced)
      .attr('fill', "yellow")
      .attr("stroke", "orange")
      .style("stroke-width", "3px")
  
    });

  
</script>
