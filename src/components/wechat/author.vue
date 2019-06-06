<template>
    <div class="page">
        <!-- <h1 style="font-size:24px;">微信授权页面</h1> -->
    </div>
</template>
<script>
import Qs from "qs";
import guestApi from "@/api/carOwner/guest";
import { getToken, setToken } from "@/utils/auth";
import { isEmptyObject, getUrlParams } from "@/utils/common";
export default {
    data() {
        return {
            query: this.$route.query,
            urlParams: getUrlParams(),
            wechatScope: {
                base: "snsapi_base", // snsapi_base （不弹出授权页面，直接跳转，只能获取用户openid）
                userinfo: "snsapi_userinfo" // snsapi_userinfo （弹出授权页面，可通过openid拿到昵称、性别、所在地。并且，即使在未关注的情况下，只要用户授权，也能获取其信息）
            },
            loading: true
        };
    },
    components: {},
    created() {
        this.init();
    },
    mounted() {},
    methods: {
        notFound() {
            this.$router.replace("/notFound");
        },
        init() {
            let query = Qs.parse(this.query);
            if (
                isEmptyObject(query) ||
                !query.nextPath ||
                query.nextPath == "/notFound"
            ) {
                this.notFound();
                return false;
            }
            // 微信授权回来处理
            let urlParams = this.urlParams;
            let appId = this.$session.get("appId");
            if (!isEmptyObject(urlParams) && urlParams.code && appId) {
                // 微信授权回来的处理
                guestApi
                    .wxuserInfo({
                        appid: appId,
                        code: urlParams.code
                    })
                    .then(res => {
                        if (res.code == 20000) {
                            let data = res.data;
                            this.$session.set("wxUserInfo", data);
                            setToken(data.token);
                            this.$router.replace({
                                path: query.nextPath,
                                query: query
                            });
                        } else {
                            this.$toast.fail(res.msg);
                            this.notFound();
                        }
                    });
            } else {
                this.loading = this.$toast.loading({
                    duration: 0, // 持续展示 toast
                    forbidClick: true, // 禁用背景点击
                    loadingType: "spinner",
                    message: "微信授权中"
                });
                this.wxLogin();
            }
        },
        wxLogin() {
            guestApi.wxLogin().then(res => {
                if (res.code == 20000) {
                    let data = res.data;
                    let appId = data.appid;
                    this.$session.set("appId", appId);
                    this.wechatLoginAuth(appId);
                }
            });
        },
        wechatLoginAuth(appId) {
            let wechatScopeType = this.wechatScope.userinfo;
            let redirectUri = location.href;
            let data = {
                ext1: "ext1",
                ext2: "ext2"
            };
            let authUrl = this.getAuthUrl(
                appId,
                redirectUri,
                wechatScopeType,
                data
            );
            this.loading.clear();
            location.replace(authUrl);
        },
        getAuthUrl(appId, redirect_uri, scope, data) {
            let params = {
                appid: appId,
                redirect_uri: redirect_uri,
                response_type: "code",
                scope: scope,
                state: 1
            };
            let paramsString = Qs.stringify(params) + "#wechat_redirect";
            let url =
                "https://open.weixin.qq.com/connect/oauth2/authorize?" +
                paramsString;
            return url;
        }
    }
};
</script>