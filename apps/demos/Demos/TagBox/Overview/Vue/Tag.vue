<template>
  <div>
    <div
      ref="target"
      :class="{'dx-tag-content': true, 'disabled-tag': isDisabled}"
      :aria-disabled="isDisabled"
      @mouseenter="show = true"
      @mouseleave="show = false"
    >
      <img
        :src="tagData.ImageSrc"
        :alt="`${tagData.Name}. Picture`"
        class="tag-img"
      >
      <span>{{ tagData.Name }}</span>
      <div
        v-if="!isDisabled"
        class="dx-tag-remove-button"
      />
    </div>

    <DxPopover
      :visible="show"
      :target="target"
    >
      <p>
        <b>Name: </b><span>{{ tagData.Name }}</span>
      </p>
      <p>
        <b>Price: </b><span>{{ tagData.Price }}</span>
      </p>
      <p>
        <b>In-stock: </b><span>{{ tagData.Current_Inventory }}</span>
      </p>
      <p>
        <b>Category: </b><span>{{ tagData.Category }}</span>
      </p>
    </DxPopover>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue';
import DxPopover from 'devextreme-vue/popover';

type TagData = Record<string, string>;

const props = withDefaults(defineProps<{
  tagData?: TagData
}>(), {
  tagData: () => ({} as TagData),
});

const isDisabled = ref(props.tagData.Name === 'SuperHD Video Player');
const show = ref(false);
const target = ref(null);
</script>
<style scoped>
.dx-tag-content {
  display: flex;
  align-items: center;
}

.tag-img {
  height: 30px;
  margin-right: 5px;
}

.dx-tag-content.disabled-tag {
  padding-right: 6px;
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
