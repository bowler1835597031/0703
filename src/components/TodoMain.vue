<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li class="completed" v-for="item in list" :key="item.id">
      <div class="view">
        <input class="toggle" type="checkbox" />
        <label>任务名</label>
        <button class="destroy"></button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {

};
</script>
