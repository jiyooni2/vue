<template>
  <button class="fancy-btn">
    <slot> 대체 컨텐츠(값이 주어지지 않았을 때 작동) </slot>
  </button>

  <button>
    <slot name="main" message="안녕" />
  </button>
</template>

<style>
.fancy-btn {
  color: #fff;
  background: linear-gradient(315deg, #42d392 25%, #647eff);
  border: none;
  padding: 5px 10px;
  margin: 5px;
  border-radius: 8px;
  cursor: pointer;
}
</style>
