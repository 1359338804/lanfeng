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
            <span @click="toDetail">
              Detail
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
            <a @click="toDetail(item.id)"><img v-bind:src="item.src" /></a>
            <div class="proTitle" @click="toDetail(item.id)">{{item.title}}</div>
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
          { text: 'Fuel Dispenser', id: '01' },
          { text: 'Spare Parts', id: '02' },
          { text: 'System', id: '03' }
        ],
        systemData: [],
        isActive: 0
      }
    },
    methods:{
      toHome:function(){
				this.$router.push('/home')
			},
      toDetail:function(id){
				this.$router.push(`/details?${id}`)
      },
      change: function (index, text) {
        this.isActive = index;
        if(text == 'System'){
          this.systemData = []
          systemDatas.CentralControlSystem.map((item, index)=>{
            if(index==0){
              this.systemData.push(item)
            }
          })
          systemDatas.TankMonitorSystem.map((item, index)=>{
            if(index==0){
              this.systemData.push(item)
            }
          })
        }else if(text == 'Fuel Dispenser'){
          this.systemData = []
        }else if(text == 'Spare Parts'){
          this.systemData = []
        }
      }
		}
	}
</script>

<style lang="less" scoped="scoped">
	.main {
		width: 100%;
		.menu{
			float: left;
			width: 184px;
		}
		.banner {
			width: 100%;
			.slider {
				float: right;
				width: 766px;
        padding: 0 30px;
        padding-bottom: 20px;
        background-color: #fff;
        min-height: 616px;
        .location{
          height: 46px;
          line-height: 46px;
          color: #999;
          font-size: 13px;
          p{
            span{
              cursor: pointer;
            }
            span:hover{
              color: red;
            }
          }
        }
			}
		}
	}
</style>
