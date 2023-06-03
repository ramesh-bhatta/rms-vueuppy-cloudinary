# rms-vueuppy-cloudinary

rms-vueuppy-cloudinary is the vue js library which utilizes uppy library to upload file to the cloudinary. This library provides the dashboard uploader vue component with different options. This library depends on vue2 and uppy(^3.9.0).


# Installation
npm install rms-vueuppy-cloudinary


# How to implement example:
```
import UppyCloudinaryUpload from 'rms-vueuppy-cloudinary';

<UppyCloudinaryUpload btnTriggerClass="btnUpload" preset="" cloudName="" :allowedMetaFields="allowedMetaFieldsArr" @uploaded="uploaded">
     // if you want to pass some icons inside button slot is created
      <!-- <template v-slot:btn-icon>
        <b-icon icon="cloud-upload-alt"
        size="is-medium"></b-icon>
      </template> -->
</UppyCloudinaryUpload>

```

# Props
| Props                      | Type    | Required | Description                                                           |
|----------------------------|---------|----------|-----------------------------------------------------------------------|
| btnTriggerClass            | String  | Yes      | Button class with which uppy dashboard will triggered 
| preset                     | String  | Yes      | Your preset                                                                     |
| cloudName                  | String  | Yes      | Your cloudinary cloud name                                                                     |
| allowedMetaFields          | Array   | Optional | default:["file","name","upload_preset"]                               |
| allowMultipleUploadBatches | Boolean | Optional | default: false                                                        |
| allowedFileTypes           | Array   | Optional | default: ['image/*','video/*',"image/png']                            |
| minNumberOfFiles           | Number  | Optional | default: 1                                                            |
| maxNumberOfFiles           | Number  | Optional | default:10                                                            |
| maxFileSize                | Number  | Optional | default:40000000                                                      |
| closeModalOnClickOutside   | Boolean | Optional | default: true                                                         |
| closeAfterFinish           | Boolean | Optional | default: true                                                         |
| disableModal               | Boolean | Optional | default:false, Wheather to show dashboard uploader as popup or inline, for inline closeAfterFinish should be false  |
| tags                       | Array   | Optional | default: []                                                           |
| autoProceed                | Boolean | Optional | default: false                                                        |
| showProgressDetails        | Boolean | Optional | default:true                                                          |
| buttonText                 | String  | Optional | default: "Upload"                                                     |
| buttonClass                | String  | Optional | default: "button is-secondary"                                        |
| debug                      | Boolean | Optional | default: true                                                         |



# Vue Events
uploaded
This events will emit information about uploads.

# How to listen to events example?
```
<!-- eslint-disable vue/no-unused-components -->
<template>
  <div>
    <UppyCloudinaryUpload btnTriggerClass="btnUpload" preset="" cloudName=""  @uploaded="uploaded">
    // if you want to pass some icons inside button slot is created
      <!-- <template v-slot:btn-icon>
        <b-icon icon="cloud-upload-alt"
        size="is-medium"></b-icon>
      </template> -->
    </UppyCloudinaryUpload>
  </div>
</template>

<script>
import UppyCloudinaryUpload from './components/UppyCloudinaryUpload.vue';


  export default {
    name: "App",
    components: { UppyCloudinaryUpload },
    data(){
      return {
        cloudName:'<your cloudinary cloudname',
        preset: '<your preset>'
      }
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

```
