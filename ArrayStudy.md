# hahaha
ZT

众所都之，数组项在一个数组中都有自己的位置。在JavaScript中提供了两个确定数组项位置的方法：indexOf()和lastIndexOf()。今天我们主要一起学习这两个方法是如何使用，又是如何查找出数组项在数组中的确切位置。

indexOf()方法

indexOf()方法从数组的开头（位置为0）开始向后查询。indexOf()方法返回指定数组项在数组中找到的第一索引值。
如果通过indexOf()查找指定的数组项在数组中不存在，那么返回的值会是-1。

语法

indexOf()使用的语法非常的简单：

arr.indexOf(searchElement[, fromIndex = 0])
searchElement: 是指定要查找的数组项
fromIndex: 开始查找的位置。
如果该索引值(fromIndex)大于或等于数组长度(length)，意味着不会在数组里查找，返回-1。
如果参数中提供的索引值是一个负值，则将其作为数组末尾的一个抵消，即-1表示从最后一个元素开始查找，-2表示从倒数第二个元素开始查找 ，以此类推。

注意：如果参数中提供的索引值是一个负值，仍然从前向后查询数组。如果抵消后的索引值仍小于0，则整个数组都将会被查询。其默认值为0。

如果indexOf()返回的值为-1时，就可以轻松的判断这个数组项是否在数组中存在。著作权归作者所有。
值得注意的是indexOf()方法并不是所有浏览器都支持（IE9+、Firefox2+、Safari 3+、Opera 9.5+和Chrome）。
如果希望在能更好的让浏览器支持indexOf()方法，你可以在你的代码顶部添加下面的这部分代码：

if (!Array.prototype.indexOf) {
    Array.prototype.indexOf = function(elt /*, from*/) {
        var len = this.length;

        var from = Number(arguments[1]) || 0;
        from = (from < 0) ? Math.ceil(from) : Math.floor(from);
        if (from < 0) {
            from += len;
            for (; from < len; from++) {
                if (from in this && this[from] === elt) {
                    return from;
                }
            }
            return -1;
        };
    }
  } 
 
 lastIndexOf()方法
lastIndexOf()方法和indexOf()刚好相反，从一个数组中末尾向前查找数组项，并且返回数组项在数组中的索引值，如果不存在，则返回的值是-1。

语法
lastIndexOf()方法的语法规则如下：

arr.lastIndexOf(searchElement[, fromIndex = arr.length - 1])
searchElement：需要查找的数组项
fromIndex: 从数组的末尾开始向前查找，默认值为arr.length -
和indexOf()方法一样，如果fromIndex值大于或等于数组的长度(arr.length)，则整个数组会被查找。如果参数中提供的索引值是一个负值，则将其作为数组末尾的一个抵消，即-1表示从最后一个元素开始查找，-2表示从倒数第二个元素开始查找 ，以此类推。另外，如果该值为负时，其绝对值大于数组长度，则方法返回 -1，即数组不会被查找。如果值为正数，表示的是数组中对应的位置，向数组前查找。

 原文: http://www.w3cplus.com/javascript/array-part-6.html © w3cplus.com
