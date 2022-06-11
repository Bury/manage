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
      <el-button type="text" @click.stop="goDetail($index, row)">查看</el-button>
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
          label: '用户ID',
          props: 'userId',
          type: 'input',
          value: '',
          placeholder: '请输入'
        },
        {
          label: '用户姓名',
          props: 'userName',
          type: 'input',
          value: '',
          placeholder: '请输入'
        },
        {
          label: '联系方式',
          props: 'phoneNum',
          type: 'input',
          value: '',
          placeholder: '请输入'
        },
        {
          label: '实名认证',
          props: 'realName',
          type: 'select',
          value: '',
          placeholder: '请选择',
          options: [
            {label: 'AAA', value: '1'},
            {label: 'BBB', value: '2'},
            {label: 'CCC', value: '3'}
          ]
        },
        {
          label: '绑定状态',
          props: 'bandState',
          type: 'select',
          value: '',
          placeholder: '请选择',
          options: [
            {label: 'AAA', value: '1'},
            {label: 'BBB', value: '2'},
            {label: 'CCC', value: '3'}
          ]
        },
        {
          label: '注册时间',
          props: 'joinDate',
          type: 'date',
          value: '',
          placeholder: '请选择'
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
          label: '用户ID',
          visible: true,
        },
        {
          prop: 'address',
          label: '区块链地址',
          visible: true,
        },
        {
          prop: 'nickName',
          label: '昵称',
          visible: true,
        },
        {
          prop: 'userName',
          label: '用户姓名',
          visible: true,
        },
        {
          prop: 'contact',
          label: '联系方式',
          visible: true,
        },
        {
          prop: 'nftNum',
          label: 'NFT数量',
          visible: true,
        },
        {
          prop: 'approve',
          label: '实名认证',
          visible: true,
        },
        {
          prop: 'state',
          label: '绑定状态',
          visible: true,
        },
        {
          prop: 'time',
          label: '注册时间',
          visible: true,
        },
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
    goDetail(index, data){

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
