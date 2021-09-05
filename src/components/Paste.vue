<template>
  <div class="paste">
      <p style="display: flex; justify-content: space-between;">Paste in links<button @click="returnLinks">Done</button></p>
      <textarea v-model="links" name="" id="" cols="30" rows="10"></textarea>
  </div>
</template>

<script>
export default {
    name: 'Paste',
    data(){
        return{
            links: ''
        }
    },
    methods:{
        returnLinks(){
            this.$emit('links', this.links.split(','))
        }
    }
}
</script>

<style scoped>
.paste{
    color: white;

}
</style>