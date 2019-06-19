<template>
  <div @click="clickHandle">
    <!-- 如果只是展示用户头像昵称，可以使用 <open-data /> 组件 -->
    <!--<open-data type="userAvatarUrl" class="userimg"></open-data>-->
    <open-data class="username" type="userNickName"></open-data>
    <view style="margin-top: 100px;">
        <i-button @click="handleOpen4">纵向按钮，自定义颜色及图标</i-button>
    </view>
    <i-modal title="纵向排列的按钮" :visible="visible4" :actions="actions4" :action-mode="vertical" @click="handleClick4">

    </i-modal>
     <!--<i-card full title="卡片标题" extra="额外内容" thumb="https://i.loli.net/2017/08/21/599a521472424.jpg">
      <view slot="content">内容不错</view>
      <view slot="footer">尾部内容</view>
    </i-card>-->
  </div>
</template>

<script>
    import card from '@/components/card'
    import './index.css'
    var Fly = require("flyio/dist/npm/wx")
    var fly = new Fly

    export default {
        data() {
            return {
                motto: 'Hello miniprograme',
                userInfo: {
                    nickName: 'mpvue',
                    avatarUrl: 'http://mpvue.com/assets/logo.png'
                },
                visible4: false,
                actions4: [{
                    name: '按钮1'
                }, {
                    name: '按钮2',
                    color: '#ff9900'
                }, {
                    name: '按钮3',
                    icon: 'search'
                }],
            }
        },

        components: {
            card
        },

        methods: {
            getUserInfo() {
                // 必须是在用户已经授权的情况下调用
                wx.getUserInfo({
                    success: function(res) {
                        var userInfo = res.userInfo
                        var nickName = userInfo.nickName
                        var avatarUrl = userInfo.avatarUrl
                        var gender = userInfo.gender //性别 0：未知、1：男、2：女
                        var province = userInfo.province
                        var city = userInfo.city
                        var country = userInfo.country
                        console.log(userInfo)
                    }
                })
            },
            handleOpen4() {
                this.visible4 = true;
            },
            handleClick4() {
                this.visible4 = false;
            },
            bindViewTap() {
                const url = '../logs/main'
                if (mpvuePlatform === 'wx') {
                    mpvue.switchTab({
                        url
                    })
                } else {
                    mpvue.navigateTo({
                        url
                    })
                }
            },
            clickHandle(ev) {
                console.log('clickHandle:', ev)
                    // throw {message: 'custom test'}
            },
        },

        created() {
            this.getUserInfo();
            //通过用户id获取信息,参数直接写在url中
            fly.get('http://localhost:9999/news')
                .then(function(response) {
                    console.log(response);
                })
                .catch(function(error) {
                    console.log(error);
                });
            wx.hideTabBar();
            // let app = getApp()
        }
    }
</script>

<style scoped>
    .userinfo {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    
    .userinfo-avatar {
        width: 128rpx;
        height: 128rpx;
        margin: 20rpx;
        border-radius: 50%;
    }
    
    .userinfo-nickname {
        color: #aaa;
    }
    
    .usermotto {
        margin-top: 150px;
    }
    
    .form-control {
        display: block;
        padding: 0 12px;
        margin-bottom: 5px;
        border: 1px solid #ccc;
    }
    
    .all {
        width: 7.5rem;
        height: 1rem;
        background-color: blue;
    }
    
    .all:after {
        display: block;
        content: '';
        clear: both;
    }
    
    .left {
        float: left;
        width: 3rem;
        height: 1rem;
        background-color: red;
    }
    
    .right {
        float: left;
        width: 4.5rem;
        height: 1rem;
        background-color: green;
    }
</style>