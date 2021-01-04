<template>
  <div class="Pos">
    <!-- elment里的所有组件都是以el开头的 -->
    <el-row>
      <el-col :span="7" class="pos-order" id="order-list">
        <el-tabs>
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border style="width: 100%">
              <el-table-column
                prop="goodsName"
                label="商品名称"
              ></el-table-column>
              <el-table-column
                prop="count"
                label="数量"
                width="80"
              ></el-table-column>
              <el-table-column
                prop="price"
                label="金额"
                width="80"
              ></el-table-column>
              <el-table-column label="操作" width="80" fixed="right">
                <template v-slot="scope">
                  <el-button
                    type="text"
                    size="small"
                    @click="handleDetele(scope)"
                    >删除</el-button
                  >
                  <el-button type="text" size="small" @click="addOrderList(scope.row)"
                    >增加</el-button
                  >
                </template>
              </el-table-column>
            </el-table>
            <div class="totalDIV"> 
              <small> 数量：{{totalCount}}  金额：{{totalMoney}}元</small>
      
            </div>
            <div class="div-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger" @click="del">删除</el-button>
              <el-button type="success" @click="sum">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单"> 挂单dan </el-tab-pane>
          <el-tab-pane label="外卖"> 外卖 </el-tab-pane>
        </el-tabs>
      </el-col>

      <el-col :span="17">
        <div class="often-goods">
          <div class="title">常用商品</div>
          <div class="often-goods-list">
            <ul>
              <li v-for="(goods, index) in oftenGoods" :key="index" @click="addOrderList(goods)">
                <span>{{ goods.goodsName }}</span>
                <span class="o-price">￥{{ goods.price }}元</span>
              </li>
            </ul>
          </div>
        </div>

        <div class="goods-type">
          <el-tabs>
            <el-tab-pane label="汉堡">
              <div>
                <ul class="cookList">
                  <li v-for="(goods, index) in type0Goods" :key="index" @click="addOrderList(goods)">
                    <span class="foodImg"
                      ><img :src="goods.goodsImg" width="100%"
                    /></span>
                    <span class="foodName">{{ goods.goodsName }}</span>
                    <span class="foodPrice">￥{{ goods.price }}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="小食"> 
                <div>
                <ul class="cookList">
                  <li v-for="(goods, index) in type1Goods" :key="index" @click="addOrderList(goods)">
                    <span class="foodImg"
                      ><img :src="goods.goodsImg" width="100%"
                    /></span>
                    <span class="foodName">{{ goods.goodsName }}</span>
                    <span class="foodPrice">￥{{ goods.price }}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="饮料"> 
                <div>
                <ul class="cookList">
                  <li v-for="(goods, index) in type2Goods" :key="index" @click="addOrderList(goods)">
                    <span class="foodImg"
                      ><img :src="goods.goodsImg" width="100%"
                    /></span>
                    <span class="foodName">{{ goods.goodsName }}</span>
                    <span class="foodPrice">￥{{ goods.price }}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="套餐"> 
                <div>
                <ul class="cookList">
                  <li v-for="(goods, index) in type3Goods" :key="index" @click="addOrderList(goods)">
                    <span class="foodImg"
                      ><img :src="goods.goodsImg" width="100%"
                    /></span>
                    <span class="foodName">{{ goods.goodsName }}</span>
                    <span class="foodPrice">￥{{ goods.price }}元</span>
                  </li>
                </ul>
              </div> </el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>
<script>
console.log(333);
import axios from "axios";
import aaa from "../../assets/111.jpg";
export default {
  name: "Pos",
  data() {
    return {
      tableData: [],
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: [],
      totalMoney:0,
      totalCount:0
    };
  },
  // 使用钩子函数，表示一开始创建就开始拉取数据
  created:function(){
    console.log(555);
    axios.get('https://www.fastmock.site/mock/0bf6a5bae7eab8507e44b56191ddff36/vuepos/oftenGoods')
    // 用箭头函数，因为有时候操作data的值，箭头函数的this就是指向外层的this，就不会和作用域有关了
    .then(reponse=>{
      console.log(reponse);
      this.oftenGoods=reponse.data.oftenGoods;
    })
    .catch(error=>{
      console.log(error);
      // 错误处理
      alert('网络错误')
    })

    axios.get('http://rap2api.taobao.org/app/mock/274686/food12')
    // 用箭头函数，因为有时候操作data的值，箭头函数的this就是指向外层的this，就不会和作用域有关了
    .then(reponse=>{
      console.log(reponse);
      this.type0Goods=reponse.data.data[0];
      this.type1Goods=reponse.data.data[1];
      this.type2Goods=reponse.data.data[2];
      this.type3Goods=reponse.data.data[3];
    })
    .catch(error=>{
      console.log(error);
      // 错误处理
      alert('网络错误')
    })
  },
  // elment是虚拟的，所以要在所有虚拟dom加载完成之后才在钩子函数里写这个，所以选择mounted
  mounted: function () {
    var orderHeight = document.body.clientHeight;
    // console.log(orderHeight);
    document.getElementById("order-list").style.height = orderHeight + "px";
    console.log(222);
  },
  methods: {
    handleDetele(scope) {
      console.log(scope.row);
      this.tableData = this.tableData.filter((item) => {
        return item.goodsName !== scope.row.goodsName;
      });
    },
    add(scope) {
      console.log(scope);
      this.tableData.map((item) => {
        if (item.goodsName === scope.row.goodsName) {
          item.count++;
        }
        return item;
      });
      this.tableData.forEach((element)=>{
        this.totalCount+=element.count;
        this.totalMoney=this.totalMoney+(element.price*element.count)
      })
    },
    del() {
      this.tableData = [];
      this.totalMoney=0;
      this.totalCount=0
      
    },
     sum() {
       let sum =0
         this.tableData.map(item => {
        console.log(item);
        sum=sum+item.count*item.price
      })
       console.log(sum)
      if(this.totalCount!=0){
        this.tableData=[];
        this.totalCount=0;
        this.totalMoney=0;
        this.$message ({
            message:`结账成功 ${sum}`,
            type:"success"
        })
      }
      // let sum =0
      // this.tableData.map(item => {
      //   console.log(item);
      //   sum=sum+item.count*item.price
      // })
      // alert(sum)
    },
    //添加商品一定会传入一个商品的对象，goods就相当于商品的对象
    addOrderList(goods){
      this.totalMoney=0;
      this.totalCount=0
      // （1）先判断商品是否存在在列表中
      //isHave是一个判断变量
      console.log(goods);
      let isHave=false;
      for(let i=0;i<this.tableData.length;i++){
        if(this.tableData[i].goodsId==goods.goodsId){
          isHave=true;
        }
      }
      // （2）根据判断的值来编写业务逻辑
      if(isHave){
        //改变列表中商品的数量,filter用来进行过滤
        let arr = this.tableData.filter(o=>o.goodsId == goods.goodsId);
        arr[0].count++;
      }else{
        let newGoods={
          goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1
          }
          this.tableData.push(newGoods)
      }
      //计算价格汇总
      this.tableData.forEach((element)=>{
        this.totalCount+=element.count;
        this.totalMoney=this.totalMoney+(element.price*element.count)
      })
    }
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pos-order {
  background-color: #f9fafc;
  border-right: 1px solid #c0ccda;
}
::v-deep .el-tabs__nav-wrap {
  background-color: #fff;
}

.div-btn {
  margin-top: 15px;
}

.title {
  height: 20px;
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
  padding: 10px;
  text-align: left;
}

.often-goods-list ul li {
  list-style: none;
  float: left;
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 5px;
  background-color: #fff;
  cursor: pointer;
}

.o-price {
  color: #58b7ff;
}

.goods-type {
  clear: both;
  cursor: pointer;
}

.cookList li {
  list-style: none;
  width: 23%;
  border: 1px solid #e5e9f2;
  height: auot;
  overflow: hidden;
  background-color: #f9fafc;
  padding: 2px;
  float: left;
  margin: 2px;
}

.cookList li span {
  display: block;
  float: left;
}

.foodImg {
  width: 40%;
}

.foodName {
  font-size: 18px;
  padding-left: 10px;
  color: brown;
}

.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}
.totalDIV{
  background-color: #fff;
  padding: 10px;
  border-bottom:1px solid #d3dce6;
}
</style>