<template>
  <el-dropdown trigger="click" @command="handleSetSize">
    <div>
      <svg-icon class-name="size-icon" icon-class="size" />
    </div>
    <el-dropdown-menu slot="dropdown">
      <el-dropdown-item v-for="item of sizeOptions" :key="item.value" :disabled="size===item.value" :command="item.value">
        {{ item.label }}
      </el-dropdown-item>
    </el-dropdown-menu>
  </el-dropdown>
</template>

<script>
export default {
  data() {
    return {
      sizeOptions: [
        { label: 'Medium', value: 'medium' },
        { label: 'Default', value: 'small' },
        { label: 'Mini', value: 'mini' },
      ],
    };
  },
  computed: {
    size() {
      return this.$store.getters.size;
    },
  },
  methods: {
    handleSetSize(size) {
      this.$ELEMENT.size = size;
      this.$store.dispatch('app/setSize', size);
      this.refreshView();
      this.$message({
        message: 'Switch Size Success',
        type: 'success',
      });
    },
    refreshView() {
      const { fullPath } = this.$route;

      this.$nextTick(() => {
        this.$router.replace({
          path: '/redirect' + fullPath,
        });
      });
    },
  },
};
</script>
<style lang="scss" scoped>
.size-icon{
  vertical-align: -0.15em !important;
}
</style>
