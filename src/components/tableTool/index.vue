<template>
  <div class="tableTool">
    <el-table
      v-loading="loading"
      border
      fit
      highlight-current-row
      style="width: 100%"
    >
      <el-table-column
        v-for="item in columns"
        :key="item.prop"
        v-bind="{ ...item }"
        show-overflow-tooltip=""
      >
        <template slot-scope="scope">
          <img v-if="item.isImg" :src="item.url" alt="">
          <span v-else>{{ scope.row[item.prop] || "--" }}</span>
        </template>
      </el-table-column>
      <el-table-column v-if="showOperator" label="操作">
        <template slot-scope="scope">
          <slot name="operate" v-bind="scope"></slot>
        </template>
      </el-table-column>
    </el-table>
    <div v-if="isPage" class="table-tool">
      <el-pagination
        v-if="paginationOption.total > 0"
        prev-text="上一页"
        next-text="下一页"
        v-bind="paginationOption"
        @size-change="sizeChange"
        @current-change="currentChange"
        @prev-click="prevClick"
        @next-click="nextClick"
      />
      <el-button
        class="jump"
        v-if="paginationOption.total > 0"
        type="primary"
        size="mini"
        @click="goCurrentPage"
      >GO</el-button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    columnData: {
      type: Array,
      default: [],
    },
    showOperator: {
      type: Boolean,
      default: true,
    },
    paginationOption: {
      type: Object,
      default() {
        return {
          layout: "total, prev, pager, next, jumper",
          total: 0,
          "page-size": 100,
        };
      },
    },
    loading: {
      type: Boolean,
      default: false,
    },
    isPage: {
      type: Boolean,
      default: true,
    },
  },
  computed: {
    columns() {
      return this.columnData.filter((column) => {
        return column.visible;
      });
    },
  },
  data() {
    return {
      pageParam: {
        pageNum: 1,
        pageSize: 10,
      },
    };
  },
  methods: {
    goCurrentPage() {},
    sizeChange(pageSize) {
      this.pageParam.pageSize = pageSize;
      this.$emit("size-change", pageSize);
    },
    currentChange(currentPage) {
      this.pageParam.pageNum = currentPage;
      this.$emit("size-change", currentPage);
    },
    prevClick(currentPage) {
      this.pageParam.pageNum = currentPage;
      this.$emit("prev-click", currentPage);
    },
    nextClick(currentPage) {
      this.pageParam.pageNum = currentPage;
      this.$emit("next-click", currentPage);
    },
  },
};
</script>

<style lang="scss" scoped>
.table-tool{
    display: flex;
    justify-content: flex-end;
    align-items: center;
    margin-top: 20px;
}
.jump{
    margin-left: 10px;
}
</style>