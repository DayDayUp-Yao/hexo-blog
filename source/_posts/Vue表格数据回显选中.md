title: Vue表格数据回显选中
author: Yao Fei
date: 2020-12-05 16:58:36
tags: Vue
categories: 前端开发
cover: http://yfmine.work:8080/images/2.jpg
coverWidth: 1440
coverHeight: 960
---


<el-table v-loading="loading" :data="roleList" border height="300" @selection-change="handleSelectionChange1"
          ref="table" row-key="roleId">
  <el-table-column align="center" type="selection" width="55"/>
  <el-table-column align="center" type="index" label="序号" width="50"/>
  <el-table-column label="角色名称" align="center" prop="roleName"/>
</el-table>

selectRoleByUserId(params).then((response) => {
  this.userRoleList = response.data;
// 回显选中操作
  this.userRoleList.forEach(item1 => {
    this.roleList.forEach(item2 => {
      if (item1.roleId == item2.roleId) {
        //multipleTable 是这个表格的ref属性 true为选中状态
        this.$refs.table.toggleRowSelection(item2, true);
      }
    })
  })
})

