实现下拉刷新在单文件js中加入
export default{
config:{

enablePullDownRefresh:ture
}


}
在页面添加函数
onPullDownRefresh(){


}
wx.showNavigationBarLoading(Object object)
在当前页面显示导航条加载动画
wx.hideNavigationBarLoading(Object object)
