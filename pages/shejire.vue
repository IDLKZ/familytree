<template>
  <v-container>
    <vue-tree
      style="width: 100%; height: 500px; border: 1px solid gray;"
      :dataset="tree"
      :config="treeConfig"
      linkStyle="straight"
    >
      <template v-slot:node="{ node, collapsed }">

        <div
          class="rich-media-node"
          :style="{ border: collapsed ? '2px solid grey' : '' }"
        >
          <img
            :src="'http://familytree/' + node.img"
            style="width: 48px; height: 48px; border-radius: 4px;"
          />
          <span style="padding: 4px 0; font-weight: bold;"
          >{{ node.name }}</span
          >
        </div>
      </template>
    </vue-tree>
  </v-container>
</template>

<script>
  import VueTree from '@ssthouse/vue-tree-chart';
    export default {
      layout: 'layout',
        name: "shejire",
      components:{
        VueTree
      },
      data() {
        return {
          treeConfig: { nodeWidth: 140, nodeHeight: 80, levelHeight: 200, zoom: true },
          tree:{},
        }
      },

      async asyncData({$axios}) {
        let tree = await $axios.$get("/tree-family");
        return {tree}
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
