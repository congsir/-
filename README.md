# -
用于记录前端开发在实际项目中踩过的坑

#记录一次h5页面在做qq,微信分享过程中踩过的坑     2019/4/23
  # 微信分享
    #采用微信分享sdk，正确配置就好
    var data = res.data;
    wx.config({
        debug: false, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
        appId: data.appId, // 必填，公众号的唯一标识
        timestamp: data.timestamp, // 必填，生成签名的时间戳
        nonceStr: data.nonceStr, // 必填，生成签名的随机串
        signature: data.signature,// 必填，签名
        jsApiList: data.jsApiList // 必填，需要使用的JS接口列表
    });
    wx.ready(function() {
        wx.onMenuShareTimeline({ //分享到朋友圈
            title: "", // 分享标题
            desc: "", // 分享摘要
            link: window.location.href, // 分享链接
            imgUrl: "",//分享图片
            success: function() {},
            cancel: function() {}
        });
        wx.onMenuShareAppMessage({ //分享给好友
            title: "", // 分享标题
            desc: "", // 分享摘要
            link: window.location.href, // 分享链接
            imgUrl:"",
            success: function() {},
            cancel: function() {}
        });
        wx.onMenuShareQQ({
            title: "", // 分享标题
            desc: "", // 分享摘要
            link: window.location.href, // 分享链接
            imgUrl: "",
        });
    });
    
    #上述为分享的代码，但是使用后发现微信分享给好友，微信分享给朋友圈均为正常，但是分享到qq不正常
    #查阅资料，发现分享到qq，qq会使用title作为分享标题，分享页面第一张尺寸大于300x300的图片作为分享缩略图
    #并且可以采用meta配置的方法进行缩略图与描述配置
    #<meta itemprop="name" content="分享的标题"/>
    #<meta itemprop="image" content="分享的缩略图" />
    #<meta name="description" itemprop="description" content="分享的描述" />
    
    # 其中，分享的缩略图采用相对路径，分享的图片无法显示，需要使用绝对路径
