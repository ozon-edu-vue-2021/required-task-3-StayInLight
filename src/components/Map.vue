<template>
  <div class="map">
    <h3>Карта офиса</h3>

    <div v-if="!isLoading" class="map-root">
      <!-- map -->
      <MapSvg ref="svg" />
      <TableSvg v-click-outside="hide" ref="table" />
    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script>
import * as d3 from "d3";
import MapSvg from "@/assets/images/map.svg";
import TableSvg from "@/assets/images/workPlace.svg";
import tables from "@/assets/data/tables.json";
import legend from "@/assets/data/legend.json";
import people from "@/assets/data/people.json";
import ClickOutside from "vue-click-outside";

export default {
  components: {
    MapSvg,
    TableSvg,
  },
  data() {
    return {
      isLoading: false,
      svg: null,
      g: null,
      tableSvg: null,
      tables: [],
    };
  },
  mounted() {
    this.svg = d3.select(this.$refs.svg);
    this.g = this.svg.select("g");
    this.tableSvg = d3.select(this.$refs.table);

    this.tables = tables;

    if (this.g) {
      this.drawTables();
    } else {
      console.log("ERROR");
    }
  },
  methods: {
    drawTables() {
      const self = this;

      const svgTablesGroup = this.g.append("g").classed("groupedTables", true);

      this.tables.map((table) => {
        svgTablesGroup
          .append("g")
          .attr("transform", `translate(${table.x}, ${table.y}) scale(0.5)`)
          .attr("id", table._id)
          .classed("employer-place", true)
          .append("g")
          .attr("transform", `rotate(${table.rotate || 0})`)
          .attr("group_id", table.group_id)
          .html(this.tableSvg.html())
          .attr(
            "fill",
            legend.find((legendItem) => legendItem.group_id === table.group_id)
              ?.color ?? "transparent"
          )
          .on("click", function (e) {
            e.stopPropagation();
            const person =
              people.find((personItem) => personItem._id === table._id) ?? null;

            self.$emit("update:isUserOpenned", true);
            self.$emit("update:person", person);
          });
      });
    },
    hide() {
      this.$emit("update:isUserOpenned", false);
      this.$emit("update:person", null);
    },
  },
  directives: {
    ClickOutside,
  },
};
</script>

<style scoped>
.map {
  height: 100%;
  width: 100%;
  padding: 24px;
  overflow: hidden;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
}

.employer-place {
  cursor: pointer;
}

.map-root {
  height: 100%;
  width: 100%;
  overflow: hidden;
  box-sizing: border-box;
}

h3 {
  margin-top: 0px;
}

::v-deep svg {
  height: 100%;
  width: 100%;
}

::v-deep .table {
  cursor: pointer;
}
</style>
