<template>
  <div>
    <TodoHeader @add="addFn"></TodoHeader>
    <TodoMain :list="showlist" @del="delFn"></TodoMain>
    <TodoFooter
      :count="count"
      @filterdata="filterdataFn"
      @clear="clearFn"
    ></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoMain from './components/TodoMain';
import TodoFooter from './components/TodoFooter';
export default {
  data() {
    return {
      list: JSON.parse(localStorage.getItem('list')) || [],
      getSel: 'all',
    };
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods: {
    addFn(val) {
      console.log(val);
      const id = this.list[this.list.length - 1]
        ? this.list[this.list.length - 1].id + 1
        : 100;
      this.list.push({
        name: val,
        isDone: false,
        id,
      });
    },
    delFn(id) {
      const index = this.list.findIndex((ele) => ele.id == id);
      this.list.splice(index, 1);
    },
    filterdataFn(val) {
      console.log(val);
      this.getSel = val;
    },
    clearFn() {
      this.list.forEach((ele) => (ele.isDone = false));
    },
  },
  computed: {
    count() {
      return this.list.filter((ele) => !ele.isDone).length;
    },
    showlist() {
      if (this.getSel == 'no') {
        return this.list.filter((ele) => !ele.isDone);
      } else if (this.getSel == 'yes') {
        return this.list.filter((ele) => ele.isDone);
      } else {
        return this.list;
      }
    },
  },
  watch: {
    list: {
      deep: true,
      handler(val) {
        console.log(val);
        localStorage.setItem('list', JSON.stringify(val || []));
      },
    },
  },
};
</script>

<style lang="less" scoped></style>
