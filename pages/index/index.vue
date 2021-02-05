<template>
	<view>
		<ls-state-button :plain="plain" :color="color" ref="button" @submit="handleSubmit" />
		<view class="wrap">
			<view style="margin-bottom: 20rpx;">请求结果：</view>
			<radio-group @change="resultRadioChange">
				<label v-for="(item, index) in resItems" :key="index">
					<radio :value="item.value" :checked="index === resIndex" />
					{{ item.name }}
				</label>
			</radio-group>
			<view style="margin-bottom: 20rpx;margin-top: 40rpx;">成功按钮是否镂空：</view>
			<radio-group @change="plainRadioChange">
				<label v-for="(item, index) in plainItems" :key="index">
					<radio :value="item" :checked="index === plainIndex" />
					{{ item }}
				</label>
			</radio-group>
			<view style="margin-bottom: 20rpx;margin-top: 40rpx;">按钮颜色：</view>
			<radio-group @change="colorRadioChange">
				<label v-for="(item, index) in colorItems" :key="index">
					<radio :value="item.value" :checked="index === colorIndex" />
					{{ item.name }}
				</label>
			</radio-group>
			<view style="margin-top: 40rpx;">
				API调用提交：<text class="active" @click="$refs.button.submit()">点击触发提交</text>
			</view>
			<view style="margin-top: 40rpx;">
				按钮点击状态：<text class="active" @click="$refs.button.init()">重置</text>
			</view>
		</view>
	</view>
</template>

<script>
import lsStateButton from '@/components/ls-state-button/ls-state-button.vue';
export default {
	comments: { lsStateButton },
	data() {
		return {
			resItems: [
				{
					value: '1',
					name: '成功'
				},
				{
					value: '-1',
					name: '失败'
				}
			],
			resIndex: 0,
			plainItems: ['是', '否'],
			plainIndex: 1,
			colorItems: [{
				value: '#f37b1d',
				name: '桔橙'
			}, {
				value: '#39b54a',
				name: '墨绿'
			}, {
				value: '#0081ff',
				name: '海蓝'
			}, {
				value: '#e54d42',
				name: '嫣红'
			}],
			colorIndex: 1,
			color: '#39b54a'
		};
	},
	computed: {
		plain() {
			return this.plainIndex == 0
		},
	},
	methods: {
		colorRadioChange(evt) {
			for (let i = 0; i < this.colorItems.length; i++) {
				if (this.colorItems[i].value === evt.target.value) {
					this.colorIndex = i;
					break;
				}
			}
			this.color = this.colorItems[this.colorIndex].value;
		},
		plainRadioChange(evt) {
			for (let i = 0; i < this.plainItems.length; i++) {
				if (this.plainItems[i] === evt.target.value) {
					this.plainIndex = i;
					break;
				}
			}
		},
		resultRadioChange(evt) {
			for (let i = 0; i < this.resItems.length; i++) {
				if (this.resItems[i].value === evt.target.value) {
					this.resIndex = i;
					break;
				}
			}
		},
		handleSubmit() {
			setTimeout(() => {
				if (this.resIndex == 0) {
					this.$refs.button.success(() => {
						// 这里写提交成功后的代码逻辑
						console.log('提交成功');
					});
				} else {
					this.$refs.button.fail('提交失败');
				}
			}, 1600);
		}
	}
};
</script>

<style>
page {
	box-sizing: border-box;
	padding: 200rpx 30rpx 30rpx;
}
.wrap {
	padding: 20rpx;
	background-color: #f5f7fa;
	border-radius: 10rpx;
	margin-top: 100rpx;
	color: #666;
}
.active {
	color: #007AFF;
}
label+label {
	margin-left: 30rpx;
}
</style>
