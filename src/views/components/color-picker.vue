<script setup lang="ts">
import { ref, watch } from "vue";

defineOptions({
  name: "ColorPicker"
});

const size = ref("default");
const dynamicSize = ref();
const isOpen = ref(false);
const colorPickerRef = ref();

const color = ref("rgba(255, 69, 0, 0.68)");
const otherColor = ref("hsla(209, 100%, 56%, 0.73)");
const predefineColors = ref([
  "#ff4500",
  "#ff8c00",
  "#ffd700",
  "#90ee90",
  "#00ced1",
  "#1e90ff",
  "#c71585",
  "rgba(255, 69, 0, 0.68)",
  "rgb(255, 120, 0)",
  "hsv(51, 100, 98)",
  "hsva(120, 40, 94, 0.5)",
  "hsl(181, 100%, 37%)",
  "hsla(209, 100%, 56%, 0.73)",
  "#c7158577"
]);

watch(size, val =>
  val === "disabled"
    ? (dynamicSize.value = "default")
    : (dynamicSize.value = size.value)
);

function onClick() {
  isOpen.value ? colorPickerRef.value.hide() : colorPickerRef.value.show();
  isOpen.value = !isOpen.value;
}
</script>

<template>
  <el-card shadow="never">
    <template #header>
      <div class="card-header">
        <span class="font-medium">
          <el-link
            href="https://element-plus.org/zh-CN/component/color-picker.html"
            target="_blank"
            style="margin: 0 4px 5px; font-size: 16px"
          >
            颜色选择器
          </el-link>
          <br />
          <el-radio-group v-model="size" size="small">
            <el-radio label="large">大尺寸</el-radio>
            <el-radio label="default">默认尺寸</el-radio>
            <el-radio label="small">小尺寸</el-radio>
            <el-radio label="disabled">禁用</el-radio>
          </el-radio-group>
        </span>
      </div>
    </template>

    <p class="mb-2">不同尺寸、选择透明度、预定义颜色</p>
    <el-color-picker
      v-model="color"
      show-alpha
      :predefine="predefineColors"
      :size="dynamicSize"
      :disabled="size === 'disabled'"
    />
    <el-divider />

    <p class="mb-2">外部触发器</p>
    <el-space wrap>
      <el-color-picker
        ref="colorPickerRef"
        v-model="otherColor"
        show-alpha
        :predefine="predefineColors"
        :size="dynamicSize"
        :disabled="size === 'disabled'"
      />
      <el-button
        :size="dynamicSize"
        :disabled="size === 'disabled'"
        @click="onClick"
      >
        {{ isOpen ? "关闭" : "打开" }}
      </el-button>
    </el-space>
  </el-card>
</template>
