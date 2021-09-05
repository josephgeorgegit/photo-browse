<template>
<div id="app">
  <div style="position: absolute; z-index: 99999999;">
    <button class="paste-button" v-if="!open_paste" @click="paste_funk">Paste</button>
    <Paste class="paste-field" v-else @links="returnLinks"/>
  </div>
  <div id="images">
    <div 
    @click="scroll" 
    :style="{
      transform: `translateX(-${transition_properties[0]}%)`, 
      transition: `${transition_properties[1]}s`
      }" 
    style="display: flex; width: 200vw;"
    >
      <div v-for="image in two_images.slice(0, 2)" :key="image" class="container">
        <img  :src="image" alt="">
      </div>
    </div>
  </div>

</div>
</template>

<style>
body{
  background-color: #020202;
}
#images{
  display: flex;
  width: 100vw !important;
  height: 100vh;
  display: fixed;
  top: 0;
  left: 0;
  overflow-y: hidden;
}
.paste-field{
  position: fixed; 
  right: 20px; 
  top: 20px;
}
.paste-button{
  position: fixed;
  top: 20px;
  right: 20px;
}
.container{
  height: 100vh !important;
  width: 100vw !important;
  display: flex;
  justify-content: center;
  object-fit: cover;
}
img{
  object-fit: cover;
  z-index: 0;
  /* border-radius: 5px; */
}
</style>

<script>
import Paste from '@/components/Paste.vue'

export default {
  name: 'App',
  components: {
    Paste
  },
  data(){
    return{
      position: 0,
      images: [],
      queue: [0, 1, 2],
      active: false,
      open_paste: false
    }
  },
  computed: {
    two_images(){
      return [this.images[this.queue[0]], this.images[this.queue[1]], this.images[this.queue[2]]]
    },
    transition_properties(){
      if(this.active){
        return [50, 0.5]
      }
      return [0, 0]
    },
  },
  methods: {
    paste_funk(){
      this.open_paste = !this.open_paste
    },
    returnLinks(e){
      this.open_paste = false
      this.images = e
    },
    scroll(){
      this.active = true

      setTimeout(() => {
        if(this.two_images[1] == this.images[this.images.length-1]){
          this.queue = [this.images.length-1, 0, 1]
          this.active = false
          return
        }
  
        if(this.two_images[0] == this.images[this.images.length-1]){
          this.queue = [0, 1, 2]
          this.active = false
          return
        }
  
        this.queue = this.queue.map((index) => {return index + 1})
        this.active = false
        return
      }, 500)

    },
  }
}
</script>


