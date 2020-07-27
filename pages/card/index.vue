<template name="index">
	<view>
		<cu-custom bgColor="bg-gradual-pink" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">编辑卡片</block>
		</cu-custom>
		<view class="flex flex-wrap" v-for="card in cardList" :key="card">
			<view class="basis-xl bg-grey margin-xs padding-sm radius">xl(80%)</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "index",
		data() {
			return {
				index: -1,
				switchC: true,
				imgList: [],
				uploadUrl: "/sys/common/upload",
				card: {
					userId: '',
					cardNo: '',
					bank: '',
					fixedQuota: '',
					billDay: '',
					dueDay: '',
					remainQuota: ''
				},
				cardList: [1,2,3,4]
			};
		},
		methods: {
			submit() {
				let card = this.card;
				if (!card.cardNo || card.cardNo.length == 0) {
					this.$tip.alert('请输入卡号');
					return false
				}
				this.$tip.loading();
				this.$http.post('/api/card/add', this.card).then(res => {
					console.log(res)
					this.$tip.loaded();
					if (res.data.success) {
						this.$tip.toast('提交成功')
					}
				}).catch(() => {
					this.$tip.loaded();
					this.$tip.error('提交失败')
				});
			},
			cancle() {
				console.log('清空数据')
			}
		}
	}
</script>

<style>
	.uni-form-item .title {
		padding: 20rpx 0;
	}
</style>
