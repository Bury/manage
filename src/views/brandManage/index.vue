<template>
  <div class="app-container">
    <SearchTool :search-data="searchDate" @search="search" @reset="search"></SearchTool>
    <TableTool
    ref="tableTool"
    :loading="loading"
    :data="tableData"
    :column-data="columnData"
    :pagination-option="paginationOption"
    @current-change="currentChange"
    @size-change="sizeChange"
    >
    <template v-slot:operate="{$index, row}">
      <el-button type="text" @click.stop="editClick($index, row)">编辑</el-button>
      <el-button type="text" @click.stop="deleteClick($index, row)">删除</el-button>
    </template>
    </TableTool>
  </div>
</template>

<script>
import SearchTool from '../../components/searchTool/index.vue'
import TableTool from '../../components/tableTool/index.vue'
export default {
  components: {SearchTool, TableTool},
  data() {
    return {
      searchDate: [
        {
          label: '品牌方名称',
          props: 'userId',
          type: 'input',
          value: '',
          placeholder: '请输入'
        }
      ],
      formData: {},
      loading: false,
      tableData: [],
      columnData: [
        {
          prop: 'index',
          label: '序号',
          visible: true,
        },
        {
          prop: 'userId',
          label: '品牌方Logo',
          visible: true,
          isImg: true
        },
        {
          prop: 'nickName',
          label: '品牌名称',
          visible: true,
        },
        {
          prop: 'createTime',
          label: '创建时间',
          visible: true,
        },
        {
          prop: 'time',
          label: '最后操作时间',
          visible: true,
        }
      ],
      paginationOption: {
        layout: "total, prev, pager, next, jumper",
        total: 100,
        "page-size": 10,
        "current-page": 1
      }
    }
  },
  created() {
    
  },
  methods: {
    search(formData = {}){
      if(formData){
        this.formData = formData
      }else{
        this.formData = {}
      }
    },
    editClick(index, data){

    },
    deleteClick(index, data){

    },
    currentChange(current){
      this.paginationOption["current-page"] = current
    },
    sizeChange(val){
      this.paginationOption["page-size"] = val
    }
  }
}
</script>
