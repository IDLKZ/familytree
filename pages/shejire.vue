<template>
  <v-container>
    <div id="tree" ref="tree"></div>
  </v-container>
</template>

<script>
  import OrgChart from '@balkangraph/orgchart.js'
    export default {
      layout: 'layout',
        name: "shejire",
      data() {
        return {
          nodes: [

          ]
        }
      },
      methods: {
        oc: function(domEl, x) {
          this.chart = new OrgChart(domEl, {
            nodes: x,
            nodeBinding: {
              field_0: "name",
              field_1: "title",
              img_0: "img"
            },
            template: "luba",
            menu: {
              pdf: { text: "Export PDF" },
              png: { text: "Export PNG" },
            },
            nodeMenu: {
              pdf: { text: "Export PDF" },
              png: { text: "Export PNG" },
            },
          });
        },

      },

      mounted(){
        this.oc(this.$refs.tree, this.nodes)
      },
      created() {
        console.log(this.nodes)
      },
      async asyncData({$axios}) {
        const nodes = await $axios.$get("/tree-family")
        return {nodes}
        // this.$axios.$post("/data",{media: media});
      }
    }
</script>

<style scoped>
  .rich-media-node {
    width: 80px;
    padding: 8px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
    color: white;
    background-color: #388E3C;
    border-radius: 4px;
  }
</style>
