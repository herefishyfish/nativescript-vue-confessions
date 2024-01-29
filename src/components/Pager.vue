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
  pager.on("scroll", (args: any) => {
    currentIndex.value = args["currentPosition"];
    emits("updateIndex", currentIndex.value);
  });
};
</script>
<template>
  <Pager @loaded="onPagerLoaded" height="100%" peaking="30" spacing="10">
    <PagerItem>
      <Label class="font-bold text-center text-8xl text-stone-900">Vue!</Label>
    </PagerItem>
    <PagerItem>
      <StackLayout>
        <Label textWrap="true" class="font-bold text-3xl text-[#2b7750]">
          <!-- Hello Vue from NativeScript -->
          Hello, Vue!
        </Label>
      </StackLayout>
    </PagerItem>
    <PagerItem>
      <Label class="font-bold text-3xl text-blue-300">Third</Label>
    </PagerItem>
    <PagerItem>
      <Label class="font-bold text-3xl text-blue-300">Fourth</Label>
    </PagerItem>
  </Pager>
</template>
