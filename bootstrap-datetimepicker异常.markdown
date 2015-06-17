bootstrap-datetimepicker异常
=============
异常描述：将日期视图设置为月模式时，点击月份N后，高亮显示的是N+2的月份。

源码62行如下：
```javascript
this.bootcssVer = options.bootcssVer || (this.isInput ? (this.element.is('.form-control') ? 3 : 2) : ( this.bootcssVer = this.element.is('.input-group') ? 3 : 2 ));
```
这里判断bootstrap的版本。
版本为2：左右箭头标签为i
版本为3：左右箭头标签为span
而在版本为2时，以下months不包含左右箭头。months.eq(**this.date.getUTCMonth() + 2**),这里就不应该+2.
```javascript
var months = this.picker.find('.datetimepicker-months')
    .find('th:eq(1)')
	.text(year)
	.end()
	.find('span').removeClass('active');
if (currentYear == year) {
	// getUTCMonths() returns 0 based, and we need to select the next one
	months.eq(this.date.getUTCMonth() + 2).addClass('active');
}
```

解决办法：
在input的class中添加form-control样式，使得bootstra版本判断为3.
