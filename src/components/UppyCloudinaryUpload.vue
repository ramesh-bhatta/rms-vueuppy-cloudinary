<template>
    <div>
        <button v-bind:class="btnTriggerClass + ' ' + buttonClass">
            <slot name="btn-icon"></slot> {{ buttonText }}
        </button>

    </div>
</template>
  
<script>

import Uppy from "@uppy/core";
import Dashboard from "@uppy/dashboard";
import XHR from '@uppy/xhr-upload';

import "@uppy/core/dist/style.css";
import "@uppy/dashboard/dist/style.css";


export default {
    name: 'UppyCloudinaryUpload',
    props: {
        cloudName: {
            type: String,
            required: true,
        },
        preset: {
            type: String,
            required: true,
        },
        btnTriggerClass: {
            type: String,
            required: true
        },
        allowMultipleUploadBatches: {
            type: Boolean,
            default: false
        },
        minNumberOfFiles: {
            type: Number,
            default: 1,
        },
        maxNumberOfFiles: {
            type: Number,
            default: 10,
        },
        maxFileSize: {
            type: Number,
            default: 40000000,
        },
        allowedFileTypes: {
            type: Array,
            default() {
                return ['image/*', 'video/*', 'image/png'];
            },
        },
        allowedMetaFields: {
            type: Array,
            default() {
                return ["file", "name", "upload_preset"];
            }
        },
        closeModalOnClickOutside: {
            type: Boolean,
            default: true
        },
        closeAfterFinish: {
            type: Boolean,
            default: true,
        },
        disableModal: {
            type: Boolean,
            default: false,
        },
        tags: {
            type: Array,
            default() {
                return [];
            },
        },
        autoProceed: {
            type: Boolean,
            default: false,
        },
        showProgressDetails: {
            type: Boolean,
            default: true,
        },

        buttonText: {
            type: String,
            default: 'Upload',
        },
        buttonClass: {
            type: String,
            default: 'button is-secondary',
        },
        debug: {
            type: Boolean,
            default: true
        }
    },
    computed: {
        uppy: function () {
            console.log("Child :", { cloudName: this.cloudName, upload_preset: this.preset });
            return new Uppy({
                id: 'uppy',
                autoProceed: false,
                debug: this.debug,
                allowMultipleUploadBatches: this.allowMultipleUploadBatches,
                meta: {
                    upload_preset: this.preset,
                    tags: this.tags
                },
                restrictions: {
                    maxFileSize: this.maxFileSize,
                    maxNumberOfFiles: this.maxNumberOfFiles,
                    minNumberOfFiles: this.minNumberOfFiles,
                    allowedFileTypes: this.allowedFileTypes,
                }
            });
        }
    },
    mounted() {
        this.uppy.use(Dashboard, {
            inline: this.disableModal,
            trigger: `.${this.btnTriggerClass}`,
            showProgressDetails: true,
            proudlyDisplayPoweredByUppy: false,
            closeModalOnClickOutside: this.closeModalOnClickOutside,
            closeAfterFinish: this.closeAfterFinish
        }).use(XHR, {
            endpoint: `https://api.cloudinary.com/v1_1/${this.cloudName}/image/upload`,
            fieldName: "file",
            formData: true,
            allowedMetaFields: this.allowedMetaFields
        });

        // events listener
        this.uppy.on("file-added", file => {
            console.log("FILE ADDED ON DASHBOARD", file);
            this.uppy.setFileMeta(file.id, {
                file: file.data,
                upload_preset: this.preset,
                tags: this.tags
            });
        });

        // listen for response
        this.uppy.on("complete", (result) => {
            console.log("FILE UPLOAD STATUS :", { "Successful Files": result.successful, "Failed Files": result.failed });
            console.log("<<<<<<<Emit Events with full response>>>>>>");
            this.$emit('uploaded', result); // emit event along with upload response 

        });


    }

}
</script>

  
<style></style>