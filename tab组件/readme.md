# tab组件

页面:
```
    $('.tabs').each(function (index,element) {
        $(element).children('.tabs-bar').children('li').eq(0).addClass('active')
        $(element).children('.tabs-content').children('li').eq(0).addClass('active')
        })
    $('.tabs').on('click','.tabs-bar > li',function(e){
       var $li=$(e.currentTarget)
        $li.addClass('active')
        .siblings()
        .removeClass('active')
        var index = $li.index()
        console.log(index)
        var $content = $li.closest('.tabs').find('.tabs-content>li').eq(index)
        console.log($content)
        $content.addClass('active')
        .siblings()
        .removeClass('active')
    })
```

## 改进成组件

1. 原型链
```
    function Tabs(selector){
        this.elements = $(selector)
        this.init()
        this.bindEvents()
    }
    Tabs.prototype.init = function () {
        this.elements.each(function (index,element) {
        $(element).children('.tabs-bar').children('li').eq(0).addClass('active')
        $(element).children('.tabs-content').children('li').eq(0).addClass('active')
        })
    }
    Tabs.prototype.bindEvents = function () {
        this.elements.on('click','.tabs-bar > li',function(e){
        var $li=$(e.currentTarget)
        $li.addClass('active').siblings().removeClass('active')
        var index = $li.index()
        var $content = $li.closest('.tabs').find('.tabs-content>li').eq(index)
        $content.addClass('active').siblings().removeClass('active')
        })
    }
    var tabs = new Tabs('.xxx')
```

2. es6方法
```
    class Tabs{
        constructor(selector){
            this.elements = $(selector)
            this.init()
            this.bindEvents()
        }
        init(){
            this.elements.each(function (index,element) {
            $(element).children('.tabs-bar').children('li').eq(0).addClass('active')
            $(element).children('.tabs-content').children('li').eq(0).addClass('active')
            })
        }
        bindEvents(){
            this.elements.on('click','.tabs-bar > li',function(e){
            var $li=$(e.currentTarget)
            $li.addClass('active').siblings().removeClass('active')
            var index = $li.index()
            var $content = $li.closest('.tabs').find('.tabs-content>li').eq(index)
            $content.addClass('active').siblings().removeClass('active')
            })
        }
    }
    var tabs = new Tabs('.xxx')
```

## 缺点：
1. class必须按照规范，html和css之间有依赖
2. js依赖了html