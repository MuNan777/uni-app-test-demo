<template>
  <view class="content">
    <block v-for="(item, index) of msgList"
           :key="index">
      <uni-card :title="item.title"
                mode="style"
                :thumbnail="item.picUrl"
                :extra="`${item.source} ${item.ctime}`"
                note="Tips">
        {{ item.description }}
      </uni-card>
    </block>
  </view>
</template>

<script lang="ts">
import Vue from "vue";
import { topNews } from "../../api/topNewsApi";
export default Vue.extend({
  data() {
    return {
      msgList: [],
      page: 1,
      num: 10,
    };
  },
  onLoad() {
    this.getMsgList();
  },
  onReachBottom() {
    this.page++;
    this.getMsgList();
  },
  methods: {
    getMsgList() {
      return topNews({
        page: this.page,
        num: this.num,
      }).then((data: any) => {
        this.msgList.push.apply(this.msgList, data.newslist);
      });
    },
  },
});
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 200rpx;
  width: 200rpx;
  margin: 200rpx auto 50rpx auto;
}

.text-area {
  display: flex;
  justify-content: center;
}

.title {
  font-size: 36rpx;
  color: #8f8f94;
}
</style>
