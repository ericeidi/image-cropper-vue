<template>
  <div>
    <cropper
      class="cropper"
      :src="img"
      :auto-zoom="false"
      :stencil-props="{
        handlers: {},
        movable: false,
        scalable: false,
        resizable: false,
        minAspectRatio: 4 / 3,
        maxAspectRatio: 4 / 3,
      }"
      :canvas="{
        minHeight: 768,
        minWidth: 1024,
        maxHeight: 768,
        maxWidth: 1024,
      }"
      :stencil-size="{
        width: 1024,
        height: 768,
      }"
      image-restriction="stencil"
      @change="onChange"
    />

    <img :src="image" />
  </div>
</template>
<script>
import { Cropper } from "vue-advanced-cropper";
import "vue-advanced-cropper/dist/style.css";

export default {
  components: {
    Cropper,
  },
  data() {
    return {
      img: "https://images.unsplash.com/photo-1609365410564-440df2f7eb9b?crop=entropy&cs=tinysrgb&fm=jpg&ixlib=rb-1.2.1&q=80&raw_url=true&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1631",
      coordinates: {
        width: 1024,
        height: 768,
        left: 0,
        top: 0,
      },
      image: null,
    };
  },
  methods: {
    onChange({ coordinates, canvas }) {
      this.coordinates = coordinates;
      // You able to do different manipulations at a canvas
      // but there we just get a cropped image, that can be used
      // as src for <img/> to preview result
      this.image = canvas.toDataURL();
    },
  },
};
</script>

<style>
/*
	It may be necessary to set limits on the size of the cropper, otherwise the cropper image will try to fill all the available space.
*/
.cropper {
  height: 600px;
  width: 600px;
  background: #ddd;
}
</style>
