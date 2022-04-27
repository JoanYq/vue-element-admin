<template>
  <el-table
    :data="tableData"
    border
    style="width: 100%"
  >
    <el-table-column
      fixed
      prop="date"
      label="日期"
      width="150"
    />
    <el-table-column
      prop="name"
      label="姓名"
      width="120"
    />
    <el-table-column
      prop="status"
      label="状态"
      width="120"
    >
      <template slot-scope="{row}">
        <el-tag :type="row.status | statusFilter">
          {{ row.status }}
        </el-tag>
      </template>
    </el-table-column>

    <el-table-column
      fixed="right"
      label="操作"
      width="500"
    >
      <!-- <template slot-scope="{row,$index}"> -->
      <template slot-scope="{row,$index}">
        <el-button type="text" size="small" @click="handleClick(scope.row)">查看</el-button>
        <el-button type="text" size="small" @click="handleUpdate(row)">编辑</el-button>
        <el-button v-if="row.status!='on'" type="success" size="small" @click="handleStatus(row,'on')">启用</el-button>
        <el-button v-if="row.status!='off'" size="small" @click="handleStatus(row,'off')">禁用</el-button>
        <el-button v-if="row.status!='delete'" type="danger" size="small" @click="handleDelete(row,$index)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        on: 'success',
        off: 'info'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        status: 'on'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        status: 'off'
      }]//,
    // statusOptions: ['on', 'off'],
    //   temp: {
    //     id: undefined,
    //     status: 'on'
    //   }
    }
  },

  methods: {
    handleClick(row) {
      console.log(row)
    },
    handleStatus(row, status) {
      this.$message({
        message: '操作Success',
        type: 'success'
      })
      row.status = status
    },
    handleDelete(row, index) {
      var that = this
      this.$notify({
        title: 'success',
        message: '删除成功',
        type: 'success',
        duration: 2000
      })
      that.list.splice(index, 1)
    }
  }
}
</script>
