<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ count }}</strong></span
    >
    <ul class="filters">
      <li>
        <a
          :class="{ selected: isSal == 'all' }"
          href="javascript:;"
          @click="change('all')"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSal == 'no' }"
          href="javascript:;"
          @click="change('no')"
          >未完成</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSal == 'yes' }"
          href="javascript:;"
          @click="change('yes')"
          >已完成</a
        >
      </li>
    </ul>
    <button class="clear-completed" @click="clear">取消已完成</button>
  </footer>
</template>

<script>
export default {
  props: ['count'],
  data() {
    return {
      isSal: 'all',
    };
  },
  methods: {
    change(val) {
      this.isSal = val;
      this.$emit('filterdata', val);
    },
    clear() {
      this.$emit('clear');
    },
  },
};
</script>
