<template>
  <div id="app">
    <h2>vuecmf-table demo</h2>
    <vc-table :selectable="selectable" :checkbox="true"  ref="vcTable"  :header-action="headerAction" :cell-event="cellEvent" :row-action="rowAction" server="http://www.b2b.com/api/Table/index" page="page" :limit="20"  :operate-width="200"></vc-table>

  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
        selectable: function (row, index) {
            if(index % 2 == 0){
                return false;  //不允许勾选
            }else{
                return true; //可以勾选
            }

        },
        headerAction:[
            {
                event: function (selectRows) {
                    console.log(selectRows)
                },
                title: '测试',
                label: '测试',
                type: 'success',
                icon: 'fa fa-plus-circle'
            },
            {
                event: function (selectRows) {
                    console.log(selectRows)
                    alert('测试2')
                },
                title: '测试2',
                label: '测试2',
                type: 'primary',
                icon: 'fa fa-edit'
            }
        ],
        //针对自定义单元格内容的事件处理， 可借助jquery进行DOM操作和事件处理
        cellEvent: [
            function (currentList) { //currentList 为当前页列表数据
                console.log(currentList)
            }
        ],
        rowAction:[
            {
                event: function (index,row) {
                    console.log(index,row)
                },
                title: '编辑',
                type: 'success',
                icon: '',
                callback: function(index,row){  //自定义操作项内容
                    if(row.status == 10){
                        return false;  //返回false 则不替换操作按钮
                    }else{
                        return 'hello world'  //替换操作按钮内容
                    }
                }
            },
            {
                event: function (index,row) {
                    console.log(index,row)
                },
                title: '删除',
                type: 'primary',
                icon: ''
            }
        ]
    }
  },
  mounted: function () {
      this.$refs.vcTable.post('http://www.b2b.com/api/table/index',{id:'11'}).then(function (data) {
          console.log(data)
      })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
