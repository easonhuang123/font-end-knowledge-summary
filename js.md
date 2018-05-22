* 基本包装类型
    * Number
        * 转化为数字
            * Number()
            * +’123’
            * parseInt()
            * parseFloat()
        * ES6拓展
            * http://es6.ruanyifeng.com/#docs/number
        * NaN
            * https://www.jianshu.com/p/8b6ac78b5ac0
            * isNaN() vs Number.isNaN()
        * 浮点数
            * toPrecision()
                * 从左到右第一个非0数字开始
            * toFixed()
                * 从小数点后第一位开始
            * https://github.com/camsong/blog/issues/9
    * String
        * 访问字符串中的字符
            * str.charAt(1) === str[1]
        * 拼接字符串
            * str.concat(‘1’, ‘2’) // ‘012’
        * 操作字符串
            * str.slice() 第一个参数都是开始位置，第二个参数是最后一个字符后面的位置；负数时与字符串长度相加
            * str.substr()第一个参数都是开始位置，第二个参数是子串的长度；负数时第一个参数与字符串长度相加，第二个参数为0
            * str.substring()第一个参数都是开始位置，第二个参数是最后一个字符后面的位置；负数时两个参数都转化为0
        * 字符串位置
            * str.indexOf() 从头算起
            * str.lastIndexOf() 从尾算起
            * 第二个参数都是从特定字符开始搜索 str.indexOf(‘o’, 6)
        * 清除前后空格
            * str.trim()
        * 大小写转换
            * str.toLoweCase
            * str.toUpperCase
        * 模式匹配
            * str.match(/.at/) === pattern.exec(str) 返回一个数组
                * 'wwwwwwcatnatvat'.match(/.at/)
                * ["cat", index: 6, input: "wwwwwwcatnatvat", groups: undefined]
            * str.search(/.at/)
                * 'wwwwwwcatnatvat'.search(/.at/)
                * 6
            * str.replace(‘at’, ‘fff’)
                * 'wwwwwwcatnatvat'.replace(/at/g, 'fff')
                * “wwwwwwcfffnfffvfff”
            * str.split(‘,’, 2) 
                * 第一个参数是分割符
                * 第二个参数是数组长度
        * 比较
            * str.localeCompare() 比较字母表顺序前后，从左开始
                * ‘ytt’.localeCompare(‘ahh’) // 1
                * ‘ytt’.localeCompare(‘ytt’) // 0
                * ‘ytt’.localeCompare(‘zhh’) // -1 
        * ES6
            * startsWith()
            * endsWith()
            * includes()
            * Repeat(3) 参数：次数
            * 模版字符串` `
    * Boolean
        * Boolean对象和boolean值不一样，不建议使用前者
* Array数组
    * push, pop, unshift, shift
    * reverse 反转数组顺序
    * sort 排序
    * contact
    * splice
    * indexOf
    * every
    * filter
    * forEach
    * map
    * some
    * reduce 归并
    * ES6
        * from === [].slice.call(obj) 类数组对象转化为数组
        * of === [].slice.call(arguments) 将一组值转化为数组
        * copyWithin 内部复制
        * find
        * findIndex
        * fill 填充
        * entries, keys, values 遍历键值对
        * includes
    * 方法是否对原数组有影响的分析
        * https://www.jianshu.com/p/1a7c81093625
* 对象，函数，闭包，作用域，this，原型，原型链
    * 原型
    * 作用域
        * 词法作用域（js）
        * 动态作用域
    * 执行上下文
        * 全局上下文
        * 函数上下文
            * 执行过程
                * 执行上下文
                    * 形参
                    * 函数声明（只是声明哦）
                    * 变量声明（不会覆盖函数声明）
                * 代码执行（开始赋值）
    * 作用域链
        * [[scope]]
    * 变量对象VO
    * this
        * reference
    * 闭包
        * 自由变量
        ```
        var data = [];
        for (var i = 0; i < 3; i++) {
        data[i] = function () {
            console.log(i);
        };
        }

        data[0]();
        data[1]();
        data[2]();
                * 
        var data = [];

        for (var i = 0; i < 3; i++) {
        data[i] = (function (i) {
                return function(){
                    console.log(i);
                }
        })(i);
        }

        data[0]();
        data[1]();
        data[2]();
        ```
    * 参数按值传递
    * call，apply
        ```
        Function.prototype.call = function (context) {
            var context = context || window;
            context.fn = this;

            var args = [];
            for(var i = 1, len = arguments.length; i < len; i++) {
                args.push('arguments[' + i + ']');
            }

            var result = eval('context.fn(' + args +')');

            delete context.fn
            return result;
        }
        ```
        * 
        ```
        Function.prototype.apply = function (context, arr) {
            var context = Object(context) || window;
            context.fn = this;

            var result;
            if (!arr) {
                result = context.fn();
            }
            else {
                var args = [];
                for (var i = 0, len = arr.length; i < len; i++) {
                    args.push('arr[' + i + ']');
                }
                result = eval('context.fn(' + args + ')')
            }

            delete context.fn
            return result;
        }
        ```
        * call参数明确，效率更高
            * .apply在运行前要对作为参数的数组进行一系列检验和深拷贝，.call则没有这些步骤，所以运行效率高。(http://blog.leanote.com/post/walkerking/apply%E5%92%8Ccall)
            * backbone
                ``` 
                var triggerEvents = function(events, args) {
                    var ev, i = -1, l = events.length, a1 = args[0], a2 = args[1], a3 = args[2];
                    switch (args.length) {
                    case 0: while (++i < l) (ev = events[i]).callback.call(ev.ctx); return;
                    case 1: while (++i < l) (ev = events[i]).callback.call(ev.ctx, a1); return;
                    case 2: while (++i < l) (ev = events[i]).callback.call(ev.ctx, a1, a2); return;
                    case 3: while (++i < l) (ev = events[i]).callback.call(ev.ctx, a1, a2, a3); return;
                    default: while (++i < l) (ev = events[i]).callback.apply(ev.ctx, args); return;
                    }
                };
                ```
            * underscore
                ```
                var optimizeCb = function(func, context, argCount) { if (context === void 0) return func; switch (argCount) { case 1: return function(value) { return func.call(context, value); }; // The 2-parameter case has been omitted only because no current consumers // made use of it. case null: case 3: return function(value, index, collection) { return func.call(context, value, index, collection); }; case 4: return function(accumulator, value, index, collection) { return func.call(context, accumulator, value, index, collection); }; } return function() { return func.apply(context, arguments); }; };
                ```
            * ecma
    * bind
        ```
        Function.prototype.bind = function (context) {

            if (typeof this !== "function") {
            throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
            }

            var self = this;
            var args = Array.prototype.slice.call(arguments, 1);

            var fNOP = function () {};

            var fBound = function () {
                var bindArgs = Array.prototype.slice.call(arguments);
                return self.apply(this instanceof fNOP ? this : context, args.concat(bindArgs));
            }

            fNOP.prototype = this.prototype;
            fBound.prototype = new fNOP();
            return fBound;
        }
        ```
    * new
        ```
        function objectFactory() {

            var obj = new Object(),

            Constructor = [].shift.call(arguments);

            obj.__proto__ = Constructor.prototype;

            var ret = Constructor.apply(obj, arguments);

            return typeof ret === 'object' ? ret : obj;

        };
        ```
    * arguments
        * callee
    * 创建对象
    * 继承
* web API
    * BOM 浏览器对象模型
        * window 浏览器实例
            * 全局对象
            * 全局方法
            * 窗口位置大小 screenTop innerHeight
            * 打开关闭 window.open
            * setTimeout setInterval
            * alert confirm prompt
        * location
            * hash
            * host
            * hostname
            * href
            * pathname
            * port
            * protocol
            * search
            * protocol://host:port/pathname?search#hash 
        * navigator
            * 检测浏览器类型
            * userAgent: "Mozilla/5.0 (iPhone; CPU iPhone OS 11_0 like Mac OS X) AppleWebKit/604.1.38 (KHTML, like Gecko) Version/11.0 Mobile/15A372 Safari/604.1” 
        * history
            * go
            * back
            * forward
            * length
    * DOM
    * Ajax
        * XHR
        * let xhr = new XMLHttpRequest()
        * xhr属性
            * readyState
                * 0 未初始化
                * 1 启动 open
                * 2 发送 send
                * 3 接受 send中
                * 4 完成 
            * responseText：作为响应主体被返回的文本
            * responseXML
            * status: 响应HTTP状态码
            * statusText：HTTP状态说明
        * xhr方法
            * open(method, url , async = true)
            * setRequestHeader
            * send
        * xhr事件
            * onreadystatechange
            * onload等7个
        * 上传与下载进度事件
            * xhr.upload.onprogress
            * xhr.onprogress
        * https://segmentfault.com/a/1190000004322487 （完整介绍xhr）
    * promise
        
    * async / await
        * https://mp.weixin.qq.com/s/jZa0YEhUov0xqMAmDDrzfg
    * axios
        
    * 事件
        * 事件循环event loop
            * https://zhuanlan.zhihu.com/p/33058983
        * apply call
    * 存储
* 网络安全
    * HTTP协议
        * 《图解HTTP》
            * http状态码
                * 200 成功
                * 204 成功但是不返回实体，即客户端无更新
                * 206 范围请求
                * 301永久性重定向
                * 302 临时性重定向
                * 303 资源重定向了，需要使用GET方法请求新的URL，类似302
                * 304 根据条件判断 https://blog.csdn.net/netdxy/article/details/50670734
                * 307 临时重定向 类似302
                * 400 请求报文存在语法错误
                * 401 需要认证
                * 403 被服务器拒绝了
                * 500 服务器发生故障
                * 503 暂时无法处理请求，正在维护或超负荷状态
        * http缓存
            * 
            * http://www.cnblogs.com/kevin2chen/archive/2017/02/22/6431322.html
            * http://louiszhai.github.io/2017/04/07/http-cache/
            * 审批上传图片出现缓存错误图片的案例
                * 强制刷新用户缓存，更新URL地址或者给URL加上时间戳
* 网络攻击
    * XSS
        * https://mp.weixin.qq.com/s/GMA2OpBLtRTEU2E2DoE_iQ
        * https://juejin.im/post/5aa7c379518825557c012b5f
        * http://www.cnblogs.com/lovesong/p/5199623.html
    * DDos
* 性能优化
    * SEO
        * 概念
            * https://blog.csdn.net/diligentkong/article/details/72902847
            * http://www.xminseo.com/2652.html
        * 优化方向
            * 内容
            * 站内优化
                * keywords
                * title
                * description
                * 网站结构
            * 站外优化
                * 发布外链
                * sitemap
                * 站长工具
        * 好文章 https://medium.com/@coderacademy/15-seo-tips-every-front-end-developer-should-know-in-2016-d579b7cefb01
    * https://juejin.im/post/59d489156fb9a00a571d6509
* webpack
    * parcel（ https://zhuanlan.zhihu.com/p/34033344
* 同构直出SSR
* 设计模式
    * 并没有写的特别好。。。（https://github.com/ToNiQian/js-design-pattern）
* 函数式编程
    * 柯里化，闭包，高阶函数
        * 函数柯里化 闭包
            * https://github.com/mqyqingfeng/Blog/issues/42
            * add(1)(2)(3)(4)
                * http://www.css88.com/archives/5147
    * 命令式 ✖️ 声明式 ☑️
    * 函数式编程
        * https://zhuanlan.zhihu.com/p/21714695
        * https://zhuanlan.zhihu.com/p/21926955
        * https://zhuanlan.zhihu.com/p/22094473
    * http://taobaofed.org/blog/2017/03/16/javascript-functional-programing/
    * FRP 函数响应式编程 RxJS

                  





