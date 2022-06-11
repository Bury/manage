<template>
  <div class="searchTool">
    <el-form ref="formSearch" :model="formData" :rules="rules" inline>
      <template v-for="item in searchData">
        <el-form-item
          v-if="item.type == 'input'"
          :label="item.label"
          :key="item.props"
        >
          <el-input
            v-model="formData[item.props]"
            :placeholder="item.placeholder"
            @change="inputChange($event, item.props)"
          ></el-input>
        </el-form-item>
        <el-form-item
          v-if="item.type == 'select'"
          :label="item.label"
          :key="item.props"
        >
          <el-select
            v-model="formData[item.props]"
            :placeholder="item.placeholder"
            @change="selectChange($event, item.props)"
          >
            <el-option
              v-for="option in item.options"
              :key="option.value"
              :label="option.label"
              :value="option.value"
            >
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item
          v-if="item.type == 'date'"
          :label="item.label"
          :key="item.props"
        >
          <el-date-picker
            v-model="formData[item.props]"
            type="daterange"
            range-separator="-"
            start-placeholder="开始日期"
            end-placeholder="结束日期"
            :format="'yyyyMMdd'"
            :value-format="'yyyyMMdd'"
          >
          </el-date-picker>
        </el-form-item>
      </template>
    </el-form>
    <div class="search-bot">
      <el-button type="primary" size="small">导出表格</el-button>
      <div>
        <el-button type="primary" size="small" @click="search">查询</el-button>
        <el-button size="small" @click="reset">重置</el-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    searchData: {
      type: Array,
      default: [],
    },
  },
  data() {
    return {
      formData: {},
      rules: {},
    };
  },
  watch: {
    searchData: {
      handler(val) {
        this.setForm(val);
      },
      deep: true,
      immediate: true,
    },
  },
  methods: {
    inputChange(e, code) {},
    selectChange(e, code) {},
    setForm(searchData) {
      searchData.forEach((item) => {
        this.$set(this.formData, item.props, item.value);
      });
    },
    search(){
        this.$emit('search', this.formData)
    },
    reset(){
        this.$emit('search')
        this.searchData.forEach(item => {
            this.$set(this.formData, item.props, '')
        })
    }
  },
};
</script>

<style lang="scss" scoped>
.searchTool {
  margin: 20px 20px;
}
.search-bot {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>