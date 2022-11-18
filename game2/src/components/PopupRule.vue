<template lang="">
  <div class="wrapper-popup" v-bind:class="getClassPopUp">
    <div class="rule">
      <h3>Luật chơi</h3>
      <p>
        Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores sint
        dolor repudiandae maxime consectetur nam voluptas, odit neque officia in
        qui explicabo asperiores magnam blanditiis minus quaerat officiis optio
        reiciendis.
      </p>
      <button class="confirm" v-on:click="confirm()">Đã hiểu</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "popup-rule",
  props: {
    isOpenPopUp: { type: Boolean, default: false }
  },
  data() {
    return {};
  },
  methods: {
    confirm() {
      console.log('Popup Rule');
      this.$emit("handleConfirm");
    }
  },
  computed: {
    getClassPopUp: function() {
      console.log(this.isOpenPopUp);
      return {
        "open-popup": this.isOpenPopUp
      };
    }
  }
};
</script>
<style lang="">
.wrapper-popup {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.4);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
}
.wrapper-popup.open-popup {
  opacity: 1;
  visibility: visible;
}
.rule {
  width: 300px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(1.3);
  position: absolute;
  background-color: #fff;
  padding: 20px;
  font-family: Arial, Helvetica, san-serif;
}
.open-popup .rule {
  transform: translate(-50%, -50%) scale(1);
}
.rule h3 {
  margin-bottom: 10px;
}
.rule .confirm {
  border: 2px solid #333;
  background-color: #fff;
  padding: 8px 15px;
  margin-top: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
}
.rule .confirm:hover {
  color: #fff;
  background-color: #333;
}
/* Kết hợp CSS3 với Vue Js để xây dựng hiệu ứng Zoom In - Zoom Out */
</style>
