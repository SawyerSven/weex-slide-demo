<template>
    <div class="address">
        
        <scroller class="address__container">
            <div class="address__item" ref="menuItem"  v-for="(item,index) in list" @swipe="slideMenu($event,index)" :key="index" @click="chooseItem(item.id)">
                <div class="address__item__info">
                    <div class="addredd__item__info__top">
                        <text class="fs14 mr4">收货人</text>
                        <text class="fs14 mr4">测试</text>
                        <text class="fs16" style="height:50px;line-height:35px;">13113131313</text>
                    </div>
                    <div class="address__item__info__bottom">
                        <text class="fs12">测试地址</text>
                    </div>
                    <image v-if="selectData === item.id" :src="APIURL + '4.png'" class="address__item__info-active"/>
                </div>
                <text class="address__item__control">编辑</text>
                <text class="address__item__control address__item__control-delete">删除</text>
            </div>
        </scroller>
        <div class="pay__success__footer">
            <text class=" fs16 bold footer_btn white" @click="jump('AddAddress')">添加新地址</text>
        </div>
    </div>
</template>
<script>
// 引入动画
const animation = weex.requireModule("animation");
export default {
  data() {
    return {
      btnStyle: {
        backgroundColor: "#00a040",
        width: 640 + "px",
        marginTop: 20 + "px"
      },
      selectData: 1,
      list: [
        {
          id: 1,
          name: "测试",
          tel: "13113131313",
          address:
            "测试地址"
        },
        {
          id: 2,
          name: "测试",
          tel: "13113131313",
          address:
            "测试地址"
        },
        {
          id: 3,
          name: "测试",
          tel: "13113131313",
          address:
            "测试地址"
        },
        {
          id: 4,
          name: "测试",
          tel: "13113131313",
          address:
            "测试地址"
        }
      ]
    };
  },
  methods: {
    slideMenu(e, index) {
      let listItems = this.$refs.menuItem;
      let ele = this.$refs.menuItem[index];
      let direction = e.direction;
      if (direction == "left") {
        this.leftSlide(ele);
      }else if(direction == "right"){
        this.rightSlide();
      }
    },
    leftSlide(ele) {
      this.rightSlide();
      animation.transition(
        ele,
        {
          styles: {
            transform: "translateX(-300px)"
          },
          duration: 150, //ms
          timingFunction: "linear",
          needLayout: false,
          delay: 0 //ms
        }
      );
    },

    rightSlide() {
      let listItems = this.$refs.menuItem;
      for (let i = 0; i < listItems.length; i++) {
        animation.transition(
          listItems[i],
          {
            styles: {
              transform: "translateX(0px)"
            },
            duration: 150, //ms
            timingFunction: "linear",
            needLayout: false,
            delay: 0 //ms
          }
        );
      }
    },

  },
};
</script>
<style lang="less" scoped>
@import url("../../assets/less/base.less");
.address {
  flex: 1;
  position: relative;
}
.address__container {
  flex: 1;
  border-top-width: 1px;
  border-top-color: @border;
}
.pay__success__footer {
  width: 750px;
  height: 100px;
  background-color: @green;
}
.publish__need__input {
  height: 60px;
  border-width: 0;
  outline: none;
  text-align: right;
}
.address__item {
  width: 1050px;
  height: 170px;
  border-bottom-width: 1px;
  border-bottom-color: @border;
  flex-direction: row;
  flex-wrap: nowrap;
}
.address__item__info {
  width: 750px;
  height: 170px;
  padding: 40px 100px 40px 40px;
  position: relative;
}
.address__item__info-active {
  width: 44px;
  height: 44px;
  position: absolute;
  right: 30px;
  top: 50px;
}
.addredd__item__info__top {
  flex-direction: row;
}
.address__item__info__bottom {
  width: 610px;
  padding-left: 120px;
  font-size: 24px;
}
.address__item__control {
  width: 150px;
  font-size: 28px;
  color: #fff;
  line-height: 170px;
  background-color: #8c8c8c;
  text-align: center;
}
.address__item__control-delete {
  background-color: @green;
}
</style>
