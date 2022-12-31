<template>
  <view>
    <web-view :src="url"></web-view>
  </view>
</template>

<script>
import { ref } from 'vue';
import { useRouter, useLoad } from '@tarojs/taro';

export default {
  setup(){
    const url = ref('');

    useLoad(() => {
      const router = useRouter();
      url.value = router.params.url;
    })

    return {
      url
    }
  }
}
</script>

<style lang="scss">

</style>
