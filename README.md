# JavaScriptCoding
JavaScript面试算法题
包含JavaScript面试常考编程题
/**
 * 判断回文
 *
 */

function checkPlalindrome(str){
    return str === str.split('').reverse().join('');
}


/**
 * 数组去重
 *
 */

Array.prototype.unique = function (arr) {
    var temp = {},
        newArr = [];
    for(var i = 0; i < this.length; i++){
        if(!temp.hasOwnProperty(this[i])){  //!temp[this[i]]
            temp[this[i]] = this[i];
            newArr.push(this[i])
        }
    }
    return newArr
}
/**
*字符串去重
*/
String.prototype.unique = function () {
    var temp = {},
        newStr = '';
    for(var i=0;i<this.length;i++){
        if(!temp.hasOwnProperty(this[i])){
            temp[this[i]] = this[i];
            newStr += this[i]
        }
    }
    return newStr;
}
var str = '124eeerrrll'
str.unique()
function unique(arr){
    let hasObj = {},
        data = [];
    for (let item of arr){
        if(!hasObj[item]){
            hasObj[item] = true;
            data.push(item)
        }
    }
    return data;
}
// console.log(unique([1,1,2,3,45,8,0,0,6,5,1]))
/**
 * 字符串中第一个不重复的字符
 */
function test(str) {
    var temp = {};
    for (var i = 0; i<str.length;i++){
        if(temp.hasOwnProperty(str[i])){
            temp[str[i]]++
        }else {
            temp[str[i]] = 1
        }
    }
    for(var key in temp){
        if(temp[key] === 1){
            return key;
        }
    }
}

/**
 * 统计字符串中出现次数最多的字母
 *
 */
function checkMaxDuplicateChar(str) {
    if (str.length == 1){
        return str;
    }
    let charObj = {};
    for(let i=0; i<str.length;i++){
        charObj[str.charAt(i)] = !charObj[str.charAt(i)]?1:
                                  charObj[str.charAt(i)]+1;
    }
    let maxChar = [],
        maxTimes = 1;
    for (let item in charObj){
        if(charObj[item] > maxTimes){
            maxChar = [];
            maxChar.push(item)
            maxTimes = charObj[item]
        }else if(charObj[item] == maxTimes){
            maxChar.push(item)
        }
    }
    return [maxTimes,maxChar];
}
// console.log(checkMaxDuplicateChar('aqqwweretretrre'))


/**
 * 自定义原型方法unshift
 */
Array.prototype.myUnshift1 = function () {
    var pos = 0;
    for (var i = 0;i < arguments.length; i++){
        this.splice(pos, 0, arguments[i]);
        pos++;
    }
    return this.length;
}
Array.prototype.myUnshift2 = function () {
    //将类数组arguments转化为数组
    var argArr = Array.prototype.slice.call(arguments);
    var newArr = argArr.concat(this);//因为是原型上的方法，this就是arr
    return newArr;
}

    /**
     * 数组按照元素的字节数排序
     * Unicode 0-255 1个字节   256-   2个字节
     */
    var arr = []
    function getBytes(str){
        var bytes = str.length;
        for (var i=0;i<str.length;i++){
            if(str.charCodeAt(i) > 255){
                bytes++
            }
        }
        return bytes;
    }
    arr.sort(function (a, b) {
        return getBytes(a) - getBytes(b);
    })

/**
 * 封装myTypeof
 * number string boolean object funtion undefined
 * new String('1')->object string
 * new Number(1)、new Boolean(1)同理
 *
 */

function myTypeof(val){
    var type = typeof val,
        toStr = Object.prototype.toString;
    var res = {
        '[object Array]': 'array',
        '[object Object]': 'object',
        '[object Number]': 'object number',
        '[object String]': 'object string',
        '[object Boolean]': 'object boolean',
    }
    if(val == null) {
        return null
    } else if(type == 'object') {
        var ret = toStr.call(val);
        return res[ret];
    }

    return type;
}

/**
 * 闭包
 */

function Test(a, b, c) {
    var d = 0;
    this.a = a;
    this.b = b;
    this.c = c;

    function e() {
        d++;
        console.log(d)
    }
    this.f = e;
}
var test1 = new Test();
test1.f();   //1
test1.f();   //2
var test2 = new Test();
test2.f();    //1

var test = function a() {
    return 'a'
}

console.log(typeof(a))  //undefined 因为外界无法访问a,一般不给函数名，但是如果函数内部需要递归，就给函数名
console.log(test.name) //a  如果不给函数名   打印test
