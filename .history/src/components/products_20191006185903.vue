<template>
	<div class="main">
		<div class="banner">
			<div class="menu">
				<menu-wrap></menu-wrap>
			</div>
			<div class="slider">
        <div class="location">
          <p>
            <span @click="toHome">
              Home
            </span>
            <span>»</span>
            <span @click="toProducts">
              Products
            </span>
          </p>
        </div>
        <ul class="typelist clearfix">
          <li class="li1" v-for="(item, index) in items" :key="item.id" :class="{ 'active': isActive==index }" @click="change(index, item.text)">
            <span>{{ item.text }}</span>
          </li>
        </ul>
        <ul v-if="this.systemData.length>0">
          <li v-for="(item, index) in systemData" class="goods_list" :key="index">
            <a @click="toDetail"><img v-bind:src="item.src" /></a>
            <span @click="toDetail">{{item.title}}</span>
          </li>
			  </ul>
			</div>
		</div>
	</div>
</template>

<script>
  import MenuWrap from '@/components/menu.vue'
  import systemDatas from '../../static/SystemData.json';
	export default {
		components: {
			MenuWrap
    },
    data() {
      return{
        items: [
          { text: 'Fuel Dispenser', id: '1' },
          { text: 'Spare Parts', id: '2' },
          { text: 'System', id: '3' }
        ],
        systemData: [],
        isActive: 0
      }
    },
    methods:{
			toHome:function(){
				this.$router.push('/home')
			},
			toProducts:function(){
				this.$router.push('/products')
      },
      toDetail:function(){
				this.$router.push('/details')
      },
      change: function (index, text) {
        this.isActive = index;
        if(text == 'System'){
          systemDatas.CentralControlSystem.map((item, index)=>{
            if(index==0){
              this.systemData.push(item)
            }
          })
        }
      }
		}
	}
</script>

<style lang="less" scoped="scoped">
	.main {
		width: 100%;
		overflow: hidden;
		.menu{
			float: left;
			width: 184px;
			overflow: hidden;
		}
		.banner {
			width: 100%;
			overflow: hidden;
			.slider {
				float: right;
				width: 766px;
        padding: 0 30px;
        padding-bottom: 20px;
        background-color: #fff;
        min-height: 416px;
        overflow: hidden;
        .location{
          height: 46px;
          line-height: 46px;
          color: #999;
          font-size: 13px;
          p{
            span:hover{
              color: red;
            }
          }
        }
        .typelist{
          position: relative;
          z-index: 99;
          padding-bottom: 20px;
          li {
            float: left;
            position: relative;
            margin-right: 10px;
            display: inline;
            width: 224px;
            background: #454545;
            line-height: 36px;
            cursor: pointer;
            span{
              color: #fff;
              margin-left: 7px;
              margin-right: 12px;
              font-size: 12px;
              text-decoration: none;
            }
          }
          .active{
            background: red;
            color: #fff;
          }
        }
        .goods_list{
          padding-top: 5px;
          margin-top: 2px;
          li {
            float: left;
            width: 210px;
            margin-right: 10px;
            margin-bottom: 8px;
            position: relative;
            overflow: hidden;
            a {
              display: block;
              width: 100%;
              overflow: hidden;
              img {
                  border: 1px #e9e9e9 solid;
              }
              span{
                line-height: 42px;
                text-align: center;
                font-size: 12px;
                font-weight: bold;
                overflow: hidden;
              }
            }
          }
        }
			}
		}
	}
</style>
