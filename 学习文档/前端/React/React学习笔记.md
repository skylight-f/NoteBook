# react-router

- BrowserRouter 浏览器自带的 h5 api ，restful风格，需要配合后台
- HashRouter 路径中有#
- MemoryRouter 在内存中管理history，地址栏不会变化，在reactNative中使用

1. 如果有一个组件，希望任何路由都显示时，把path设置为”/“
2. 路由匹配默认是模糊匹配，匹配上了就会渲染，当多个路由匹配了，则多个component都会渲染，可以使用exact关键字进行精确匹配，使用switch组件，匹配一个路由之后就不在往后匹配
3. 设置没有path的路由，则没有匹配时就会渲染此路由
