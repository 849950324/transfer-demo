<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld />
  <transfer
    v-model="selectIds"
    :data="dataList"
    style="
      text-align: left;
      display: inline-block;
      --el-transfer-panel-width: 25vw;
    "
    filterable
    :props="{
      key: 'key',
      label: 'name',
    }"
    :item-size="30"
    :titles="['虚拟列表-可选', '虚拟列表-已选']"
    :button-texts="['添加', '移除']"
    :format="{
      noChecked: '${total}',
      hasChecked: '${checked}/${total}',
    }"
    @change="handleChange"
  >
    <template #default="{ option }">
      <span class="flex">
        <span>{{ option.name }}</span>
        <span style="color: #909399; font-size: 13px">{{ option.label }}</span>
      </span>
    </template>
  </transfer>
  <!-- <el-transfer
    v-model="selectIds"
    style="text-align: left; display: inline-block; --el-transfer-panel-width:25vw"
    filterable
    :props="{
      key: 'key',
      label: 'name',
    }"
    :titles="['官方-可选', '官方-已选']"
    :button-texts="['添加', '移除']"
    :format="{
      noChecked: '${total}',
      hasChecked: '${checked}/${total}',
    }"
    :data="dataList"
    @change="handleChange"
  >
    <template #default="{ option }">
      <span class="flex">
        <span>{{ option.name }}</span> 
        <span style="color:#909399; font-size: 13px;">{{ option.label }}</span>
      </span>
    </template>
  </el-transfer> -->
  
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import transfer from "./components/transfer/index";

//穿梭器option
interface transferOption {
  key: number;
  label: string;
  name?: string;
  disabled?: boolean;
}

const dataList = ref<Array<transferOption>>([]);
const selectIds = ref<Array<any>>([])

onMounted(async() => {
  setTimeout(() => {
    for (let i = 0; i < 10000; i++) {
      let item = {
        key: i,
        label: `选项${i}`,
        name: `选项${i}`,
      }

      dataList.value.push(item);
    }
  })
  getPageLoadTime()


})

// 在页面加载完成后调用该函数，可以获取到页面渲染时间
function getPageLoadTime() {
  var startTime = performance.now();
  window.addEventListener('load', function() {
    var endTime = performance.now();
    var loadTime = endTime - startTime;
    console.log('页面渲染时间为：' + loadTime + '毫秒');
  });
}

function handleChange(
  value: number[] | string[],
  direction: "left" | "right",
  movedKeys: string[] | number[]
) {
  console.log("操作:", value, direction, movedKeys);
}

</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
.flex{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
:deep(.el-checkbox:last-of-type){
  margin-right: 30px;
}

</style>
