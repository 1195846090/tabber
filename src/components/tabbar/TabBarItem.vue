<template>
<div class="tab-bar-item" @click="itemClick">
<!--    <i class="iconfont ">&#xe609;</i>-->
<!--    <div>首页</div>-->
    <span v-if="!isActive" ><slot name="item-icon"></slot></span>
    <span v-else><slot name="item-icon-active"></slot></span>
    <div :style="activeStyle"><slot name="item-text"></slot></div>

</div>
</template>

<script>
    import "../../assets/img/tabber/iconfont.css";
    export default {
        name: "TabBarItem",
        props: {
            path: String,
            activeColor: {
                type: String,
                default: 'pink'
            }
        },
        data(){
            return{
                // isActive: true
            }
        },
        computed: {
           isActive() {

               //判断当前激活的路径是否与app.vue的item传过来的路径相同
               return this.$route.path.indexOf(this.path) !== -1
           },
            activeStyle(){
               return this.isActive ? {color: this.activeColor} : {}
            }
        },
        methods: {
            itemClick() {
               this.$router.replace(this.path).catch(err => err)
            }
        }
    }
</script>

<style scoped>
    .tab-bar-item{
        flex:1;
        text-align: center;
        height: 49px;
        font-size: 12px;
    }
    .tab-bar-item i{
        width: 24px;
        height: 24px;
        font-size: 24px;

    }
    .tab-bar-item div{
        margin-top: 3px;
    }

</style>