<template>
  <div class="selectWrap">
    <div class="select-wrapper">
      <div class="select" 
        @click="triggerOption"
        :class="{active: select_active}"  
      >
        <div class="select-content">{{selectContent.text}}</div>
        <div class="triangle-wrapper"></div>
      </div>
      <div class="option-wrapper" style="display: none;">
        <div
          class="option-item"
          v-for="(item,index) in subject"
          :key="index"
          @mouseout="out($event)"
          @mouseover="move($event)"
          @click="choose(item)"
        >{{item.text}}</div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return{
      select_active:false,
    }
  },
  props: {
    selectWidth: {
      type: Number,
      default: 100
    },
    subject: {
      type: Array,
      default: function() {
        return [];
      }
    },
    selectContent: {
      type: Object,
      default: function() {
        return { value: 0, text: "请选择" };
      }
    }
  },
  mounted() {
    document.querySelector(".selectWrap").style.width = this.selectWidth + "px";
  },
  computed: {
    optionWrapper() {
      return document.querySelector(".option-wrapper");
    },
    selectCon() {
      return document.querySelector(".select-content");
    },
    subjectList() {
      return document.getElementsByClassName("option-item");
    }
  },
  methods: {
    // option移入事件
    move(event) {
      for (var item of this.subjectList) {
        item.classList.remove("hover");
      }
      event.currentTarget.classList.add("hover");
    },
    // option移除事件
    out(event) {
      event.currentTarget.classList.remove("hover");
    },
    // selective选中事件
    triggerOption() {
      this.select_active = true;
      if (this.optionWrapper.style.display == "none") {
        this.optionWrapper.style.display = "block";
      } else {
        this.optionWrapper.style.display = "none";
      }
      for (var item of this.subjectList) {
        if (item.innerHTML == this.selectContent.text) {
          item.classList.add("hover");
        } else {
          item.classList.remove("hover");
        }
      }
    },

    // option选中事件
    choose(item, value) {
      this.select_active = false;
      this.selectContent.text = item.text;
      this.optionWrapper.style.display = "none";
      this.$emit(
        "changeSelect",
        this.selectContent.text,
        this.selectContent.value
      );
    }
  }
};
</script>

<style scope>
.select-wrapper{
  width: 100%;
  position: relative;
}
.select {
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  padding-right: 10px;
  min-width: 80px;
  width: 100%;
  height: 40px;
  line-height: 40px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  cursor: default;
  font-size: 13px;
  padding-left: 15px;
  padding-right: 15px;
  border-radius: 4px;
}
.select-wrapper .active{
  border:1px solid #0773FC;
}
.select-content {
  text-align: left;
  font-size: 14px;
  color: rgba(0, 0, 0, 0.8);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.triangle-wrapper {
  width: 18px;
  height: 100%;
  background-color: #fff;
  cursor: default;
  background: url(./img/select.png) no-repeat center;
  background-size: 14px 14px;
}

.option-wrapper {
  position: absolute;
  overflow: hidden;
  min-width: 80px;
  width: 100%;
  height:  160px;
  background: #ffffff;
  box-shadow: 0 8px 16px 0 rgba(7, 17, 27, 0.08);
  border-radius: 4px;
  overflow: auto;
}
.option-item {
  min-width: 80px;
  height: 32px;
  line-height: 32px;
  padding-right: 10px;
  text-align: left;
  cursor: default;
  font-size: 14px;
  color: rgba(0, 0, 0, 0.8);
  padding-left: 15px;
}
.option-item :hover {
  background: #f7f8f9;
}
.hover {
  background: #f7f8f9;
}


</style>