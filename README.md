
# 动效状态按钮(ls-state-button)

#### 带有提交动画效果的按钮，支持 `H5` `vue` `app`

## 说明
这是一个[uniapp](https://uniapp.dcloud.io/)项目，基于Vue 2.0
通常用于表单提交的提交按钮，它带有提交中以及提交成功的状态动画，既可以给用户一个友好的提交等待提示，又可以防止用户重复点击。


## 用法示例

```html
<ls-state-button ref="button" @submit="handleSubmit" />
```

```js
import lsStateButton from '@/components/ls-state-button/ls-state-button.vue';
export default {
	components: {
		lsStateButton
	},
	methods: {
		handleSubmit() {
			// 模拟接口请求
			setTimeout(() => {
				// 如果接口调用成功
				this.$refs.button.success(() => {
					// 这里写提交成功后的代码逻辑
					console.log('提交成功');
				});
				
				// 如果接口调用失败
				// this.$refs.button.fail('提交失败');
			}, 1600);
		}
	}
}
```
	
## 组件参数
|  属性名   | 类型  | 默认值  | 说明  |
|  ----  | ----  | ----  |
| color  | `String` | #19cc95 | 按钮主题颜色 |
| font-color  | `String` | #ffffff | 文字颜色 |
| shadow  | `Boolean` | true | 是否显示按钮阴影 |
| text  | `String` | 提交 | 按钮文字 |
| plain  | `Boolean` | false | 结果符号是否镂空 |
| submit | `Function` |   | 按钮点击后的回调  |


## 组件方法
|  方法名   |  说明  | 方法参数 |  注  |
|  ----  | ----  |
| init()  |  初始化按钮状态  | 无 | 此方法会将按钮初始化至点击前的状态 |
| success(callback)  |  提交成功  | `Function` | 此方法会将按钮状态置为成功，此方法接收一个回调方法，具体用法请看下方`success方法参数说明` |
| fail(toast)  |  提交失败  | `String` | 此方法会将按钮状态置为失败，此方法接收一个`String`类型的参数，如果不为空，失败时会一并弹出指定的toast提示 |


#### success方法参数说明
success方法接收一个回调方法，回调方法中执行你提交成功后的代码逻辑（写在这里的原因是可以保证按钮的成功动画可以充分执行完毕）。 例如如下场景：表单提交后页面跳转到列表页，

错误的使用方法： **Bad !**
```js
handleSubmit() {
		// 模拟接口请求
		setTimeout(() => {
			this.$refs.button.success();
			// 成功后跳转页面
			// 执行效果： 提交成功动画没有执行完毕，页面就已经跳走了
			uni.navigateTo({
				url: 'list'
			})
		}, 1600);
	}
```

正确的使用方法：**Good !**
```js
handleSubmit() {
		// 模拟接口请求
		setTimeout(() => {
			this.$refs.button.success(() => {
				// 成功后跳转页面
				// 执行效果：提交成功动画执行完毕，页面跳转
				uni.navigateTo({
					url: 'list'
				})
			});
		}, 1600);
	}
```


## 鸣谢
组件示例项目中，按钮的4种颜色出自高颜值css组件库[ColorUI](https://ext.dcloud.net.cn/plugin?id=239)，感谢[ColorUI](https://ext.dcloud.net.cn/plugin?id=239)！


## 谢谢