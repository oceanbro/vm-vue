<template>
  <el-container>
    <el-aside style="width: 200px;margin-top: 20px">
      <switch></switch>
    </el-aside>
    <el-main>
      <Resident class="residents-area"></Resident>
    </el-main>
  </el-container>
</template>

<script>
  import Resident from './Resident'
  export default {
    name: 'AppResident',
    components: {Resident}
  }
</script>

<style scoped>
  .residents-area {
    width: 990px;
    margin-left: auto;
    margin-right: auto;
  }
</style>

