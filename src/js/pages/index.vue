<template>
    <wxc-tab-bar
        :tab-titles="tabTitles"
        :tab-styles="tabStyles"
        title-type="icon"
        @wxcTabBarCurrentTabSelected="wxcTabBarCurrentTabSelected">
    <!-- 第一个页面内容-->
    <div class="item-container" :style="contentStyle">
        <text>首页</text>
        <wxc-button text="Test" @wxcButtonClicked="wxcButtonClicked"></wxc-button>
    </div>

    <!-- 第二个页面内容-->
    <div class="item-container" :style="contentStyle">
        <text>特别推荐</text>
    </div>

    <!-- 第三个页面内容-->
    <div class="item-container" :style="contentStyle">
        <text>消息中心</text>
    </div>

    <!-- 第四个页面内容-->
    <div class="item-container" :style="contentStyle">
        <text>我的主页</text>
    </div>
  </wxc-tab-bar>
</template>

<script>
import { WxcButton, WxcTabBar, Utils } from 'weex-ui'
import Config from './config'
export default {
    components: {
        WxcButton,
        WxcTabBar
    },
    data() {
        return {
            tabTitles: Config.tabTitles,
            tabStyles: Config.tabStyles
        }
    },
    beforeCreate: function () {
        var domModule = weex.requireModule('dom');

        domModule.addRule('fontFace', {
            fontFamily: 'iconfont-eros',
            'src': 'url(\'bmlocal://iconfont/iconfont-eros.ttf\')'
        });
    },
    created () {
        const tabPageHeight = Utils.env.getPageHeight()
        // 如果页面没有导航栏，可以用下面这个计算高度的方法
        // const tabPageHeight = env.deviceHeight / env.deviceWidth * 750
        const { tabStyles } = this
        this.contentStyle = { height: (tabPageHeight - tabStyles.height) + 'px' }
    },
    methods: {
        wxcButtonClicked (e) {
            this.$router.open({
                name: 'test'
            })
        },
        wxcTabBarCurrentTabSelected (e) {
            const index = e.page;
        }
    }
}
</script>

<style lang="sass">
    .item-container {
        width: 750px;
        background-color: #f2f3f4;
        align-items: center;
        justify-content: center;
    }
</style>
