<script setup lang="ts">
import { onLaunch, onShow, onHide } from "@dcloudio/uni-app";

onLaunch(() => {
  console.log("onLaunch");
});
onShow(() => {
  console.log("onShow");
});
onHide(() => {
  console.log("onHide");
});
</script>
