<template>
  <v-card>
      <v-flex xs12 sm10>
        <v-tree url="/item/category/list"
                :isEdit="isEdit"
                @handleAdd="handleAdd"
                @handleEdit="handleEdit"
                @handleDelete="handleDelete"
                @handleClick="handleClick"
        />
      </v-flex>
  </v-card>
</template>

<script>
  export default {
    name: "category",
    data() {
      return {
        isEdit:true
      }
    },
    methods: {
      handleAdd(node) {

        this.$http({
          method: 'post',
          url: '/item/category',
          data: this.$qs.stringify(node)
        }).then(() => {
          this.$message.success("保存成功！");
        })
          .catch(() => {
            this.$message.error("保存失败！");
          });

      },
      handleEdit(id, name) {


        console.log("edit... id: " + id + ", name: " + name)
      },
      handleDelete(id) {
        this.$http.delete("/item/category/" + id)
          .then(({}) => {
            this.$message.success("删除成功！");
          });
        console.log("delete ... " + id)
      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
