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
    * 
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
        * promise
        * async / await
    * 事件
        * 事件循环event loop
            * https://zhuanlan.zhihu.com/p/33058983
        * apply call
    * 存储
                  





