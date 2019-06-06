<template>
    <div class="page">
        <div class="main-container">
            <div class="button-content" :class="{buttonFixed:isFixed}">
                <van-button
                    native-type="button"
                    type="info"
                    :style="styleButton"
                    size="large"
                    :block="true"
                    @click="qrCodeView"
                    ref="buttonSelector"
                >查看二维码</van-button>
            </div>
            <van-row :class="{'bottom-fixed-hide':!isFixed}" :style="styleButtonFixed"></van-row>

            <van-popup v-model="show" class="qr-code-canvas-popup" :lazy-render="false">
                <canvas id="qrCodeCanvas" class="qr-code-canvas" v-show="show==true"></canvas>
            </van-popup>
        </div>
    </div>
</template>
<script>
import QRCode from "qrcode";
export default {
    name: "qrCodeReport",
    data() {
        return {
            show: false,
            // 固定底部悬浮按钮自定义样式
            styleButton: {},
            // 固定底部悬浮按钮默认样式
            styleButtonFixed: {}
        };
    },
    props: {
        qrCodeLink: {
            type: String,
            default: ""
        },
        background: {
            type: String,
            default: "#46aef7"
        },
        isFixed: {
            type: Boolean,
            default: false
        }
    },
    mounted() {
        this.init();
        this.styleButtonHandle();
        this.useQrcode();
    },
    methods: {
        init() {
            let buttonHeight = this.$refs.buttonSelector.offsetHeight + 10;
            this.styleButtonFixed = {
                height: buttonHeight + "px"
            };
        },
        qrCodeView() {
            // console.log("qrCodeView");
            if (this.show) {
                this.show = false;
            } else {
                this.show = true;
            }
        },
        useQrcode() {
            const _this = this;
            const canvas = document.getElementById("qrCodeCanvas");
            // console.log(canvas);
            // console.log(_this.qrCodeLink);
            // With promises
            QRCode.toCanvas(
                canvas,
                _this.qrCodeLink || "",
                { width: 180, margin: 1 },
                function(error) {
                    if (error) console.error(error);
                    // console.log("QRCode success!");
                }
            );
        },
        /**
         * @Description: 样式处理
         * @Param:
         * @Author: qjy
         * @LastEditors: qjy
         * @LastEditTime: Do not edit
         * @return:
         * @Date: 2019-05-16 09:46:49
         */
        styleButtonHandle() {
            this.styleButton = {
                "background-color": this.background,
                border: "1px solid" + this.background
            };
        }
    }
};
</script>
<style lang="less" scoped>
.page {
    .buttonFixed {
        position: fixed;
        left: 0;
        right: 0;
        bottom: 0;
        padding: 10px;
    }
    .bottom-fixed {
        height: 60px;
    }
    .bottom-fixed-hide {
        display: none;
    }
}
.qr-code {
    width: 240px;
    height: 240px;
}
.qr-code-canvas-popup {
    // width: 180px;
    // height: 180px;
    overflow: hidden;
}
</style>

