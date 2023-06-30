<template>
 <div class="container">
  <vue-avatar-editor 
    @finished="saveClicked"
    :width=400
    :height=400
    >
  </vue-avatar-editor>
  <img ref="image">
  <p>{{ imgSrc }}</p>
  <button @click="downloadFile">download</button>

</div>
</template>

<script>
import VueAvatarEditor from 'vue-avatar-editor-improved';

export default {
    data () {
        return {
            imgSrc: null
        };
    },
    components: {
        VueAvatarEditor: VueAvatarEditor
    },
    methods: {
        saveClicked: function saveClicked(img) {
            this.$refs.image.src = img.toDataURL();
            this.imgSrc = img
        },
        downloadFile() {
          this.imgSrc.toBlob(function(blob){const a = document.createElement("a");
          document.body.appendChild(a);
          const url = window.URL.createObjectURL(blob);
          a.href = url;
          a.download = 'blabla';
          a.click();
          a.remove();}, 'image/jpeg', 0.95);
          
        }
    }
};
</script>
<style >
  .container {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
  }
</style>