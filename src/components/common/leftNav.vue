<template>
    <div class="left-nav">
        <ul>
            <li>
                <i class="icon iconfont icon-cart-full"></i>
                <div>收银</div>
            </li>
            <li>
                <i class="icon iconfont icon-home"></i>
                <div>店铺</div>
            </li>
            <li>
                <i class="icon iconfont icon-turkey"></i>
                <div>商品</div>
            </li>
            <li>
                <i class="icon iconfont icon-diamonds"></i>
                <div>会员</div>
            </li>
            <li>
                <i class="icon iconfont icon-star"></i>
                <div>统计</div>
            </li>
            <li>
                <i class="icon iconfont icon-wreath"></i>
                <div>设置</div>
            </li>
        </ul>
    </div>
</template>
<script>
    export default {
        
    }
</script>
<!-- 不加scope，让样式在每个页面都管用 -->
<style>
    .left-nav{
        /* 给图标颜色 */
        color:#fff;
        /* 给图标字体大小 */
        font-size: 10px;
        /* 给图标一个高，能在页面100%显示 */
        height: 100%;
        background-color: #1D8CE0;
        float: left;
        /* 只在页面宽度展示5% */
        width: 5%;
    }
    /* 写icon的样式 */
    .iconfont{
        font-size: 24px;
    }
    .left-nav ul{
        padding: 0px;
        margin: 0px;
    }
    .left-nav li{
        /* 本来有点，要把点去掉 */
        list-style: none;
        /* 字体对齐方式 */
        text-align: center;
        border-bottom: 1px solid #20a0ff;
        padding: 10px;
    }

</style>