<template >
  <van-popup
    transition="popup"
    :value="value"
    @input="(val) => this.$emit('input', val)"
    closeable
    round
    position="center"
    class="address-popup"
  >
    <div class="title">选择地址</div>
    <!-- 列表 -->
    <van-list
      class="list"
      v-if="addressList"
      v-model="loading"
      :finished="finished"
      @load="getAllAddressList"
    >
      <van-radio-group v-model="select">
        <transition-group name="item" tag="div">
          <!-- 地址卡片 -->
          <div
            class="items"
            v-for="(item, i) in addresses"
            :key="item.id"
            @click="clickItem(item?.id, i)"
          >
            <address-card class="v-card v-click" :item="item" :readonly="true">
              <template #right-icon>
                <van-radio
                  icon-size="0.5rem"
                  :name="item.id"
                  checked-color="var(--tip-color2)"
                ></van-radio>
              </template>
            </address-card>
          </div>
        </transition-group>
      </van-radio-group>
    </van-list>
    <button @click="submitAddress" class="v-btn">确定</button>
  </van-popup>
</template>
<script>
import AddressCard from "./AddressCard.vue";
export default {
  components: { AddressCard },
  props: ["addressList", "value", "defaultAddress"],
  name: "SelectAddress",
  data() {
    return {
      active: 0,
      select: "",
      // 加载
      show: false,
      loading: false,
      finished: false,

      addresses: [], // 最终的元素
    };
  },
  methods: {
    // 获取全部地址
    getAllAddressList() {
      this.loading = true;
      this.select = this.addressList[0].id;
      this.addressList.forEach((p) => {
        if (p.isDefault) {
          this.select = p.id;
          this.addresses.unshift(p);
        } else {
          this.addresses.push(p);
        }
      });
      if (this.addressList.length === this.addresses.length) {
        this.finished = true;
      }
    },

    clickItem(id, i) {
      this.select = id;
      this.active = i;
    },

    submitAddress() {
      this.$emit("changeAddress", this.addresses[this.active]);
      this.$emit("input", false);
    },
  },
  watch: {},
};
</script>
<style scoped>
.address-popup {
  width: 94%;
  height: 80vh;
  padding: 0.5rem;
  display: flex;
  flex-direction: column;
}
.address-popup .list {
  overflow-y: auto;
  padding: 0.1rem;
}
.address-popup > .title {
  font-size: 0.48rem;
  font-weight: 600;
  text-align: center;
  margin-bottom: 0.5rem;
}
.v-click:active {
  transform: scale(0.99);
  box-shadow: none;
}
.address-popup .v-btn {
  width: 90%;
  position: absolute;
  left: 5%;
  bottom: 0.3rem;
  text-align: center;
  margin: 0.2rem 0;
}
</style>