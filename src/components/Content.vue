<script lang="ts" setup>
import { Pager, PagerItem } from "@nativescript-community/ui-pager";
import { registerElement, ref } from "nativescript-vue";
import { LoadEventData } from "@nativescript/core";

registerElement("Pager", () => Pager);
registerElement("PagerItem", () => PagerItem);

let currentIndex = ref(0);
const emits = defineEmits(["updateIndex"]);

const onPagerLoaded = (args: LoadEventData) => {
  const pager = args.object as Pager;
  console.log("Pager loaded");
  pager.on("scroll", (args: any) => {
    currentIndex.value = args["currentPosition"];
    emits("updateIndex", currentIndex.value);
  });
};
</script>
<template>
  <Pager @loaded="onPagerLoaded" class="w-full h-full" peaking="30" android:spacing="10">
    <PagerItem>
      <StackLayout verticalAlignment="center">
        <Label class="card font-bold text-center text-8xl text-stone-900 m-0 p-0">Vue!</Label>
      </StackLayout>
    </PagerItem>
    <PagerItem>
      <StackLayout>
        <Label textWrap="true" class="font-bold text-8xl text-stone-900">
          <!-- Hello Vue from NativeScript -->
          Hello, Vue!
        </Label>
      </StackLayout>
    </PagerItem>
    <PagerItem>
      <Label class="font-bold text-3xl text-stone-900">Third</Label>
    </PagerItem>
    <PagerItem>
      <Label class="font-bold text-3xl text-stone-900">Fourth!!</Label>
    </PagerItem>
  </Pager>
</template>

<style>
  .card {
    /*   // renderer.setClearColor(0xf0fdf4); */
    /* background-color: rgba(255, 255, 255, 0.8); */
    border-radius: 10;
  }
</style>
