<script lang="ts" setup>
import {
ref
} from 'nativescript-vue';
import Canvas from './Canvas.vue';
import Content from './Content.vue';

const progress = ref(0);
const updateProgress = (newProgress: number) => {
  progress.value = newProgress;
};
</script>

<template>
  <Frame>
    <Page>
      <ActionBar>
        <Label text="NativeScript ❤️ Vue" class="font-bold text-lg" />
      </ActionBar>

      <GridLayout rows="*">
        <Canvas :progress="progress" />
        <Content @updateIndex="updateProgress" />
      </GridLayout>
    </Page>
  </Frame>
</template>
