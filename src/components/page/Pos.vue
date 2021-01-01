<template>
    <div class="Pos">
      <!-- elment里的所有组件都是以el开头的 -->
      <el-row>
        <el-col :span='7' class="pos-order" id="order-list">
          <el-tabs>
            <el-tab-pane label='点餐'>
              <el-table>
                <el-table-column prop='goodsName' label='商品名称'></el-table-column>
                <el-table-column prop='count' label='数量'width='80'></el-table-column>
                <el-table-column prop='price' label='金额'width='80'></el-table-column>
                <el-table-column label='操作' width='80'></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label='挂单'>
              挂单
            </el-tab-pane>
            <el-tab-pane label='外卖'>
              外卖
            </el-tab-pane>
          </el-tabs>
        </el-col>
        <el-col>
          我是产品栏
        </el-col>
      </el-row>
    </div>
  </template>
  <script>
  export default {
    name: 'Pos',
    // elment是虚拟的，所以要在所有虚拟dom加载完成之后才在钩子函数里写这个，所以选择mounted
    mounted:function(){
        var orderHeight=document.body.clientHeight;
        // console.log(orderHeight);
        document.getElementById('order-list').style.height=orderHeight+'px'
    }
  }
  </script>
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
    .pos-order{
      background-color: #F9FAFC;
      border-right: 1px solid #C0CCDA;
    }
  </style>