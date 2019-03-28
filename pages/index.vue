<template lang="pug">
  div
    img(id="cropperIMG" style="max-width: 100%" src="../static/CropperTest.png")
    v-btn(depressed small @click="setBorderedDiv") Cut
    div(v-for="item,idx in borderedDiv" 
    :key="idx" 
    :style="{ borderStyle: 'solid', borderColor: 'red', width: item.width + 'px', height: item.height + 'px', position: 'absolute', left: item.left + 'px', top: item.top + 'px' }")
</template>

<script>
// import '/node_modules/cropperjs⁩/dist/cropper.css'
import Cropper from 'cropperjs'

export default {
  mounted() {
    this.setCropper()
  },
  data() {
    return {
      cropper: {},
      borderedDiv: []
    }
  },
  methods: {
    setCropper() {
      const imageDOM = document.getElementById('cropperIMG')
      let that = this
      this.cropper = new Cropper(imageDOM, {
        aspectRatio: 1 / 1
      })
    },
    setBorderedDiv() {
      let oBoxData = this.cropper.getCropBoxData()
      this.borderedDiv.push({
        width: oBoxData.width,
        height: oBoxData.height,
        left: oBoxData.left,
        top: oBoxData.top
      })
    }
  }
}
</script>
