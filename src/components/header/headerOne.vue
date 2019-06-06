<template>
    <div class="header-one">
        <van-nav-bar
            :z-index="999"
            :fixed="isFixed"
            :class="{'clear-background':backgroundStatus, 'border-bottom':isborderBottom}"
            :border="true"
            :title="title"
            :left-text="leftText"
            :right-text="rightText"
            :left-arrow="leftArrow"
            @click-left="onClickLeft()"
            @click-right="onClickRight"
        >
            <van-icon
                v-if="rightText=='icon'"
                slot="right"
                color="#000"
                :name="iconName"
                class="icon-right"
            />
        </van-nav-bar>
        <van-row :class="{'header-fixed-margin':isFixed,'header-fixed-margin-hide':!isFixed}"></van-row>
    </div>
</template>
<script>
import { NavBar, Icon } from "vant";
import back from "@/utils/back";
export default {
    name: "HeaderOne",
    data() {
        return {};
    },
    components: {
        [NavBar.name]: NavBar,
        [Icon.name]: Icon
    },
    props: {
        title: {
            type: String,
            default: ""
        },
        isFixed: {
            type: Boolean,
            default: false
        },
        backgroundStatus: {
            type: Boolean,
            default: false
        },
        leftText: {
            type: String,
            default: ""
        },
        rightText: {
            type: String,
            default: ""
        },
        leftArrow: {
            type: Boolean,
            default: true
        },
        // 是否重写事件
        onClickLeftStatus: {
            type: Boolean,
            default: false
        },
        isborderBottom: {
            type: Boolean,
            default: false
        },
        iconName: {
            type: String,
            default: "share"
        }
    },
    mounted() {},
    methods: {
        onClickLeft() {
            if (this.onClickLeftStatus) {
                this.$emit("onClickLeft");
            } else {
                back.handle();
            }
        },
        onClickRight() {
            this.$emit("onClickRight");
        }
    }
};
</script>
<style lang="less">
.header-one {
    z-index: 999;
    .van-nav-bar__left {
        top: -2px;
        left: 5px;
        .van-icon {
            font-size: @font-lg;
            color: @black;
        }
    }
    .clearBackground {
        background: transparent;
    }
    .header-fixed-margin {
        margin-top: 46px;
    }
    .header-fixed-margin-hide {
        display: none;
    }
    .icon-right {
        font-size: 20px;
    }
    .icon-right-hide {
        display: none;
    }
    .border-bottom {
        border-bottom: solid 3px #e14732;
    }
}
</style>