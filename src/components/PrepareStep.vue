<template>
    <v-container class="d-flex justify-space-between flex-column flex-grow-1">
        <div class="mb-10 mt-n4" v-if="usbSupported">
            <h6 class="text-h6 pb-4">Prepare your device</h6>

            <div class="text-body-1">
                <p>
                    This is an easy way to install
                    {{ $root.$data.OS_NAME }} on your device
                </p>
            </div>
        </div>

        <div class="mb-10 mt-n4" v-else>
            <h6 class="text-h6 pb-4 red--text text--darken-4">
                Your browser isn’t supported
            </h6>

            <div class="text-body-1">
                <p>
                    Unfortunately, you can’t use this web installer for
                    {{ $root.$data.OS_NAME }} because your browser doesn’t
                    support WebUSB. Only Google Chrome and other browsers based
                    on Chromium, such as Brave and Microsoft Edge, are supported.
                </p>
            </div>

            <div class="text-body-1 mt-4">
                <p>
                    If you think this is a mistake, update your browser to the
                    latest version and try again.
                </p>
            </div>
        </div>

        <div class="d-flex justify-space-between flex-row-reverse">
            <v-btn
                color="primary"
                @click="emit('nextStep')"
                :disabled="!usbSupported"
            >
                Start
                <v-icon dark right>mdi-arrow-right</v-icon>
            </v-btn>
        </div>
    </v-container>
</template>

<script>
export default {
    props: ["device", "blobStore", "active"],

    data: () => ({
        usbSupported: "usb" in navigator,
    }),
    
    inject: ['emit', 'saEvent'],

    watch: {
        active: {
            async handler(newState) {
                if (newState) {
                    this.saEvent("step_prepare");
                }
            },
            immediate: true,
        },
    },
};
</script>
