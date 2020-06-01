<template>
        <ul>
            <li 
                v-for="(menu,index) in data"
                :key="menu[defaultProps.label]"
               
            >
                <i class="iconfont"
                    :class="{
                        'icon-right':!isShow[index],
                        'icon-down':isShow[index]
                    }"
                    v-if="menu[defaultProps.children]"
                ></i>
                <span @click="showHide(index)">{{menu[defaultProps.label]}}</span>
                <keep-alive>
                    <tree-menu
                        v-if="isShow[index] && menu[defaultProps.children]"
                        :data="menu[defaultProps.children]"/>
                </keep-alive>
            </li>
        </ul>
</template>

<script>
export default {
    name:"tree-menu",
    props:{
        data:{
            type:Array,
            required:true
        },
        defaultProps:{
            type:Object,
            default:()=>{
                return {
                    label:"label",
                    children:"children"
                }
            }
        }
    },
    data(){
        return{
            isShow:[false,false,false],
        }
    },
    methods:{
        showHide(index){
            const flag=!this.isShow[index];
            this.$set(this.isShow,index,flag)
        }
    }
}
</script>

<style scoped>
@import "./assets/font.css";

li{
    list-style:none;
    cursor: pointer;
}
li .iconfont{
    color: #c0c4cc;
    font-size: 12px;
    margin-right: 5px;
    vertical-align: middle;
}
li span{
    font-size: 14px;
    color: #606266;
    vertical-align: middle;
}

</style>