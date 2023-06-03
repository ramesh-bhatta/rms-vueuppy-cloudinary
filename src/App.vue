<!-- eslint-disable vue/no-unused-components -->
<template>
  <div>
    <UppyCloudinaryUpload 
    :btnTriggerClass="'up1'" 
    :preset="upload_preset" 
    :cloudName="cloud_name"
     :allowedMetaFields="allowedMetaFieldsArr"
     :buttonText="'Modal Uploader'"
      @uploaded="uploaded">
      <!-- <template v-slot:btn-icon>
        <b-icon icon="cloud-upload-alt"
        size="is-medium"></b-icon>
      </template> -->
    </UppyCloudinaryUpload>
    <UppyCloudinaryUpload 
    :btnTriggerClass="'up2'"
     :disableModal="true"
      :closeAfterFinish="false"
       :preset="upload_preset"
        :cloudName="cloud_name" 
        :allowedMetaFields="allowedMetaFieldsArr"
        :buttonText="'Inline Uploader'"
         @uploaded="uploaded">
      <!-- <template v-slot:btn-icon>
        <b-icon icon="cloud-upload-alt"
        size="is-medium"></b-icon>
      </template> -->
    </UppyCloudinaryUpload>
  </div>
</template>

<script>
import UppyCloudinaryUpload from './components/UppyCloudinaryUpload.vue';
import {cloudinary} from './config.js'; // config file needs to be created inside src folder by copying config.example.js



  export default {
    name: "App",
    components: { UppyCloudinaryUpload },
    data(){
      return {
        allowedMetaFieldsArr:[
          "file", "name", "upload_preset", "tags"
        ],
        cloud_name:null,
        upload_preset:null
      }
    },
    created(){
      console.log("test ",cloudinary);
      this.cloud_name=cloudinary.cloudName;
      this.upload_preset=cloudinary.preset;
     
    },
    methods:{
      uploaded(results){
        console.log("UPLOADED status ",{results});
      }
    }
}
</script>

<style lang="scss" scoped>

</style>