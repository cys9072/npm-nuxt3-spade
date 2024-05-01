<script setup>
const MAX_VALUE = 100000;

const barValue = ref(0);
const progressPosition = ref(null);
const toolBox = ref(null);
const test = reactive({});

const btns = [{ val: 0 }, { val: 1000 }, { val: 5000 }, { val: 10000 }, { val: 50000 }, { val: 90000 }, { val: 95000 }, { val: MAX_VALUE }];

const onClickBtn = (e) => {
  const per = (e.val / MAX_VALUE) * 100;
  barValue.value = per;
};

watchEffect(() => {
  if (toolBox.value) {
  }
  if (test) {
    console.log("test", test.value);
  }
});

onUpdated(() => {
  if (toolBox.value) {
    nextTick(() => {
      console.log(toolBox.value.getBoundingClientRect().x);
      test.value = toolBox.value.getBoundingClientRect();
    });
  }
});
</script>
<template>
  <div class="page-inner">
    <!-- <p>{{ testRef }}</p> -->
    <div class="btn-wrap">
      <button v-for="btn in btns" :key="btn.val" class="btn" type="button" @click="onClickBtn(btn)">
        {{ btn.val }}
      </button>
    </div>

    <div class="progress-wrap">
      <div ref="toolBox" class="tool-box" :style="{ left: barValue + '%' }"></div>
      <div class="tool-box pointer" :style="{ left: barValue + '%' }"></div>

      <progress ref="progressPosition" class="progress" :value="barValue" :max="100"></progress>
    </div>
  </div>
</template>
<style scope>
body,
html {
  width: 100%;
  height: 100%;
}
* {
  box-sizing: border-box;
}

.page-inner {
  width: 100%;
  height: 100%;
}

/* Btn css */
.btn-wrap {
  display: flex;
  gap: 10px;
  padding: 20px;
  width: 100%;
  flex-wrap: wrap;
}
.btn {
  min-width: 100px;
  border: none;
  padding: 10px;
  border-radius: 20px;
  background: orange;
}

/* progress */
.progress-wrap {
  background-color: green;
  display: block;
  position: relative;
  padding-top: 20px;
  height: 100px;
}
.progress {
  width: 100%;
}
.tool-box {
  width: 50px;
  height: 20px;
  background: blue;
  position: absolute;
  top: 0;
  left: 22%;
  /* transform: translateX(-50%); */
  transition: 0.2s;
}

.tool-box.pointer {
  background: red;
  top: 50%;
}

.progress {
  transition: 0.2s;
  -webkit-appearance: none;
}

.progress::-webkit-progress-bar {
  background-color: grey;
  transition: 0.2s;
}
.progress::-webkit-progress-value {
  background-color: #000;
  transition: 0.2s;
}
</style>
