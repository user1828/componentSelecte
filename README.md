# componentSelecte
公共组件封装使用
1、下载组件
2、引用组件 import inputComponent from '路径'
3、使用组件


组件的参数：
1、selectWidth ：
	传入select选择框的宽度设置宽度
	传入Number类型
2、subject ：
	传入option类型
	传入Array类型
	[
		{
			title:'指定的标识',
			text:'内容',
			status:'状态'
		},
	]
	
3、changeSelect
	传入函数，触发回调函数，父组件获取选择的数据
	传入类型：函数

