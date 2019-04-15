<template>
  <div class="sankey">
    <div id="chart"></div>
  </div>
</template>

<script>
import * as d3 from 'd3'
require('../libraries/sankey.js').default(d3)

export default {
  mounted () {
    const chartBox = d3.select('#chart').node().getBoundingClientRect()

    let margin = null
    if (window.innerWidth < 480) { // mobile
      margin = {top: 100, right: 10, bottom: 30, left: 35}
    } else {
      margin = {top: 160, right: 20, bottom: 30, left: 70}
    }

    const width = chartBox.width - margin.left - margin.right,
        height = chartBox.height - margin.top - margin.bottom

    const svg = d3.select('#chart')
      .append('svg')
        .attr('viewBox', '0 0 ' + chartBox.width + ' ' + chartBox.height)
        .attr('width', width + margin.left + margin.right)
        .attr('height', height + margin.top + margin.bottom)
      .append('g')
        .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')

    const sankey = d3.sankey().size([width, height])

    if (window.innerWidth < 480) { // mobile
      sankey.nodeWidth(9)
            .nodePadding(9)
    } else {
      sankey.nodeWidth(13)
            .nodePadding(13)
    }

    var path = sankey.link()

    d3.json('Sankey.json', data => {
      // link nodes by node names
      var nodeMap = {}
      data.nodes.forEach(x => { nodeMap[x.name] = x })
      data.links = data.links.map(x => {
        return {
          source: nodeMap[x.source],
          target: nodeMap[x.target],
          value: x.value
        }
      })

      const formatNumber = d3.format(',.0f'),
        format = d => { return formatNumber(d) },
        color = d3.scale.category20()

      sankey
        .nodes(data.nodes)
        .links(data.links)
        .layout()

      const link = svg.append('g')
        .selectAll('.link')
          .data(data.links)
        .enter().append('path')
          .attr('class', 'link')
          .attr('d', path)
          .style('stroke-width', d => {
            return Math.max(1, d.dy)
          })
          .style('stroke', d => { return d.source.color })
          .sort((a, b) => { return b.dy - a.dy })

      const node = svg.append('g')
        .selectAll('.node')
          .data(data.nodes)
        .enter().append('g')
          .attr('class', 'node')
          .attr('transform', d => {
            return 'translate(' + d.x + ',' + d.y + ')'
          })
        .call(d3.behavior.drag()
          .origin(d => { return d })
          .on('dragstart', () => { this.parentNode.appendChild(this) })
          .on('drag', dragmove))

      node.append('rect')
          .attr('height', sankey.nodeWidth())
          .attr('width', d => { return d.dy })
          .style('fill', d => {
            if (d.color == undefined)
            return d.color = color(d.name.replace(/ .*/, '')) //get new color if node.color is null
            return d.color
          })
          .append('title')
          .text(d => { return d.name + '\n' + format(d.value) })

      node.append('text')
          .attr('text-anchor', 'middle')
          .text(d => { return d.name })
          .style('fill', '#C0CAC9')
          .attr('x', d => { return d.dy / 2 })
          .attr('y', (d, i) => {
            if (window.innerWidth < 480) { // mobile
              if (i < 5) { // top text
                return sankey.nodeWidth() * -4
              } else { // bottom text
                return sankey.nodeWidth() * 3
              }
            } else {
              if (i < 5) { // top text
                return sankey.nodeWidth() * -2.5
              } else { // bottom text
                return sankey.nodeWidth() * 3
              }
            }
          }).call(wrap)

    node.append('text')
        .attr('text-anchor', 'middle')
        .text(d => { return d.pov })
        .style('fill', '#E1EDF4')
        .attr('x', d => { return d.dy / 2 })
        .attr('y', (d, i) => {
          if (i >= 5) {
            if (window.innerWidth < 480) { // mobile
              return sankey.nodeWidth() * -1
            } else {
              return sankey.nodeWidth() * -0.5
            }
          }
        })

      // select elements from https://stackoverflow.com/questions/28390754/get-one-element-from-d3js-selection-by-index
      node.filter((d, i) => { return i < 5 }) // only the top nodes
          .append('svg:image')
          .attr({'xlink:href': d => { return d.image }})
          .attr('x', d => {
            if (window.innerWidth < 480) { // mobile
              return (d.dy - 50) / 2
            } else {
              return (d.dy - 100) / 2
            }
          })
          .attr('y', () => {
            if (window.innerWidth < 480) { // mobile
              return sankey.nodeWidth() * -11.2
            } else {
              return sankey.nodeWidth() * -12
            }
          })
          .attr('width', () => {
            if (window.innerWidth < 480) { // mobile
              return '50px'
            } else {
              return '100px'
            }
          })
          .attr('height', () => {
            if (window.innerWidth < 480) { // mobile
              return '50px'
            } else {
              return '100px'
            }
          })

      function dragmove(d) {
        //d3.select(this).attr('transform', 'translate(' + d.x + ',' + (d.y = Math.max(0, Math.min(height - d.dy, d3.event.y))) + ')')
        d3.select(this).attr('transform', 'translate(' + (d.x = Math.max(0, Math.min(width - d.dy, d3.event.x))) + ',' + d.y + ')')
        sankey.relayout()
        link.attr('d', path)
      }

      // wrap text from https://stackoverflow.com/questions/24784302/wrapping-text-in-d3
      function wrap(text) {
        let width
        if (window.innerWidth < 480) { // mobile
          width = 45
        } else {
          width = 100
        }
        text.each(function () {
          var text = d3.select(this),
              words = text.text().split(/\s+/).reverse(),
              word,
              line = [],
              lineNumber = 0,
              lineHeight = 1.1, // ems
              x = text.attr("x"),
              y = text.attr("y"),
              dy = 0, //parseFloat(text.attr("dy")),
              tspan = text.text(null)
                          .append("tspan")
                          .attr("x", x)
                          .attr("y", y)
                          .attr("dy", dy + "em");
          while (word = words.pop()) {
            line.push(word)
            tspan.text(line.join(" "))
            if (tspan.node().getComputedTextLength() > width) {
                line.pop()
                tspan.text(line.join(" "))
                line = [word]
                tspan = text.append("tspan")
                            .attr("x", x)
                            .attr("y", y)
                            .attr("dy", ++lineNumber * lineHeight + dy + "em")
                            .text(word)
            }
          }
        })
      }
    })
  }
}
</script>

<style lang='scss'>
.sankey {
  height: 80vh;
  width: 100%;
  max-width: 900px;
  margin: 0 auto;

  @media (max-width: 480px) {
    height: 50vh;
  }

  #chart {
    height: 100%;
    width: 100%;

    .node rect {
      cursor: move;
      fill-opacity: .9;
      shape-rendering: crispEdges;
    }

    .node text {
      pointer-events: none;
      font-family: 'PT Sans', sans-serif;
      font-size: 15px;
      line-height: 1.3em;
    }

    .node image {
    }

    .link {
      fill: none;
      stroke-opacity: .6;
    }

    .link:hover {
      stroke-opacity: 1;
    }

    /* mobile */
    @media (max-width: 480px) {
      .node text {
        font-size: 13px;
      }
    }
  }
}
</style>
