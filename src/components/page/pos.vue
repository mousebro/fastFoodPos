<template>
    <div class="pos">
        <el-row class="pos-order" >
            <el-col :span="7" id="order-list">
                <el-tabs>
                    <el-tab-pane label="点餐" prop="order">
                    <el-table :data="tableData" border show-summary style="width: 100%" >
                        <el-table-column prop="goodsName" label="商品"  ></el-table-column>
                        <el-table-column prop="count" label="数量" width="50"></el-table-column>
                        <el-table-column prop="price" label="金额" width="70"></el-table-column>
                        <el-table-column  label="操作" width="100" fixed="right">
                            <template slot-scope="props">
                                <el-button type="text" size="small" @click="addProduct()">删除</el-button>
                                <el-button type="text" size="small" @click="addProduct(props)">增加</el-button>
                            </template>
                        </el-table-column>

                    </el-table>   
                        <el-button type="warning" >挂单</el-button>
                        <el-button type="danger" >删除</el-button>
                        <el-button type="success" @click="checkout" >结账</el-button>
                    </el-tab-pane> 
                    <el-tab-pane label="挂单" prop="gudan">挂单</el-tab-pane> 
                    <el-tab-pane label="外卖" prop="waimai">外卖</el-tab-pane> 
                </el-tabs>
            </el-col>
            <el-col :span="17">
                <div >
                    <div class="often-goods">
                        <div class="title">常用商品</div>
                        <div class="often-goods-list">
                            <ul>
                                <li v-for='item in oftenGoods' :key="item.goodsId" @click="addProduct(item)">
                                    <span>{{item.goodsName}}</span>
                                    <span class="o-price">&yen;{{item.price}}元</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <div class="goods-type">
                        <el-tabs>
                            <el-tab-pane label="汉堡" prop="first">
                                <ul class='cookList'>
                                    <li v-for="item in type0Goods" :key="item.goodsId"  @click="addProduct(item)">
                                        <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                        <span class="foodName">{{item.goodsName}}</span>
                                        <span class="foodPrice">￥{{item.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label="小食" prop="second">配置管理</el-tab-pane>
                            <el-tab-pane label="饮料" prop="third">角色管理</el-tab-pane>
                            <el-tab-pane label="套餐" prop="fourth">定时任务补偿</el-tab-pane>
                        </el-tabs>
                    </div>
                </div>
            </el-col>
       </el-row>
 


    </div>
</template>
<script>
export default {
    name:"pos",
    data(){
        return {
            tableData: [{
                goodsId:1,
                goodsName: '可口可乐',
                price: 8.00,
                count:1
                }, {
                goodsId:2,
                goodsName: '香辣鸡腿堡',
                price: 15.00,
                count:1
                }, {
                goodsId:3,    
                goodsName: '爱心薯条',
                price: 8.00,
                count:1
                }, {
                goodsId:4,    
                goodsName: '甜筒',
                price: 8.00,
                count:1
            }],
            oftenGoods:[
                {
                    goodsId:1,
                    goodsName:'香辣鸡腿堡',
                    price:18
                }, {
                    goodsId:2,
                    goodsName:'田园鸡腿堡',
                    price:15
                }, {
                    goodsId:3,
                    goodsName:'和风汉堡',
                    price:15
                }, {
                    goodsId:4,
                    goodsName:'快乐全家桶',
                    price:80
                }, {
                    goodsId:5,
                    goodsName:'脆皮炸鸡腿',
                    price:10
                }, {
                    goodsId:6,
                    goodsName:'魔法鸡块',
                    price:20
                }, {
                    goodsId:7,
                    goodsName:'可乐大杯',
                    price:10
                }, {
                    goodsId:8,
                    goodsName:'雪顶咖啡',
                    price:18
                }, {
                    goodsId:9,
                    goodsName:'大块鸡米花',
                    price:15
                }, {
                    goodsId:20,
                    goodsName:'香脆鸡柳',
                    price:17
                }
            ],
            type0Goods:[
                {
                    goodsId:1,
                    goodsImg:"../../assets/timg.jpg",
                    goodsName:'香辣鸡腿堡',
                    price:18
                }, {
                    goodsId:2,
                    goodsImg:"../../assets/timg2.jpg",
                    goodsName:'田园鸡腿堡',
                    price:15
                }, {
                    goodsId:3,
                    goodsImg:"../../assets/timg.jpg",
                    goodsName:'和风汉堡',
                    price:15
                }, {
                    goodsId:4,
                    goodsImg:"../../assets/timg2.jpg",
                    goodsName:'快乐全家桶',
                    price:80
                }, {
                    goodsId:5,
                    goodsImg:"../../assets/timg2.jpg",
                    goodsName:'脆皮炸鸡腿',
                    price:10
                }, {
                    goodsId:6,
                    goodsImg:"../../assets/timg.jpg",
                    goodsName:'魔法鸡块',
                    price:20
                }, {
                    goodsId:7,
                    goodsImg:"../../assets/timg2.jpg",
                    goodsName:'可乐大杯',
                    price:10
                }, {
                    goodsId:8,
                    goodsImg:"../../assets/timg.jpg",
                    goodsName:'雪顶咖啡',
                    price:18
                }, {
                    goodsId:9,
                    goodsImg:"../../assets/timg2.jpg",
                    goodsName:'大块鸡米花',
                    price:15
                }, {
                    goodsId:20,
                    goodsImg:"../../assets/timg.jpg",
                    goodsName:'香脆鸡柳',
                    price:17
                }
            ],
        }
    },
    methods:{
        addProduct(item){
            let isHave=false;
            //判断是否这个商品已经存在于订单列表
            for (let i=0; i<this.tableData.length;i++){
                if(this.tableData[i].goodsId==item.goodsId){
                    isHave=true; //存在
                    //如果存在就进行数量添加
                    this.tableData[i].count++
                }else{ //如果不存在就进行添加
                    var newData = {
                    goodsId:item.goodsId,
                    goodsName:item.goodsName,
                    price: item.price,
                    count:1
                    }
                }
            }
            this.tableData.push(newData)
        },
        checkout(){
            this.tableData = [];
            this.$message({
                message: '结账成功，感谢你又为店里出了一份力!',
                type: 'success'
            });

        }
    },
    mounted(){
        var orderHeight = document.body.clientHeight;
        document.getElementById("order-list").style.height=orderHeight+"px";
    }
}
</script>
<style scoped>
    .pos-order #order-list{
        background-color:#f9fafc ;
        border-right:1px solid #ccc;
    }
    .often-goods>.title{
        text-align:left;
        padding:14px;
        background:linear-gradient(to bottom,#e8e8e3,#d0d0cd);
    }
    .often-goods-list>ul{
        list-style: none;
    }
    .often-goods-list>ul>li{
        float:left;
        padding:14px;
        background-color:#fff;
        border:1px solid #ccc;
        box-shadow: 0 0 5px #ccc;
        border-radius: 10px;
        margin:5px;
        cursor: pointer;
    }
    .often-goods-list>ul>li>.o-price{
        color:#58B7FF;
    }
    .often-goods-list>::after{
        content:"";
        display:block;
        clear:both;
    }
    .cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
       cursor:pointer;
   }
   .cookList li span{
        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
   .foodName{
       font-size: 18px;
       padding-left: 10px;
       color:brown;
   }
   .foodPrice{
       font-size: 16px;
       padding-left: 10px;
       padding-top:10px;
   }
</style>


