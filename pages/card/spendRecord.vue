<template name="card">
	<view>
		<cu-custom bgColor="bg-gradual-pink" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">编辑卡片</block>
		</cu-custom>
		<form>
			<view class="cu-form-group">
				<view class="title">卡号</view>
				<input placeholder="请输入卡号" name="input" v-model="card.cardNo"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">银行</view>
				<input placeholder="银行" name="input" v-model="card.bankz"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">固定额度</view>
				<input placeholder="固定额度" name="input" v-model="card.fixedQuota"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">账单日</view>
				<input placeholder="账单日" name="input" v-model="card.billDay"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">还款日</view>
				<input placeholder="还款日" name="input" v-model="card.dueDay"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">初始剩余额度</view>
				<input placeholder="初始剩余额度" name="input" v-model="card.remainQuota"></input>
			</view>

			<view class="padding flex flex-direction">
				<button class="cu-btn bg-blue lg" @click="submit">提交</button>
				<button class="cu-btn bg-blue lg" @click="cancle">取消</button>
			</view>
		</form>
	</view>
</template>

<script>
	export default {
		name: "card",
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
