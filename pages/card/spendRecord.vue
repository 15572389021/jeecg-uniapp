<template name="card">
	<view>
		<cu-custom bgColor="bg-gradual-pink" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">添加消费记录</block>
		</cu-custom>
		<form>
			<view class="cu-form-group">
				<view class="title">卡号</view>
				<input placeholder="请输入卡号" name="input" v-model="card.cardNo"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">银行</view>
				<!-- <input placeholder="银行" name="input" v-model="card.bank"></input> -->
				<picker mode="selector" :value="card.bank" @change="bankChange" :range='banks'>
					<view class="picker">
						{{banks[card.bank]}}
					</view>
				</picker>
			</view>
			<view class="cu-form-group">
				<view class="title">固定额度</view>
				<input placeholder="固定额度" name="input" v-model="card.fixedQuota"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">账单日</view>
				<picker mode="selector" :value="card.billDay" @change="billDateChange" :range='days'>
					<view class="picker">
						{{card.billDay}}
					</view>
				</picker>
			</view>
			<view class="cu-form-group">
				<view class="title">还款日</view>
				<picker mode="selector" :value="card.dueDay" @change="dueDateChange" :range='days'>
					<view class="picker">
						{{card.dueDay}}
					</view>
				</picker>
			</view>
			<view class="cu-form-group">
				<view class="title">初始剩余额度</view>
				<input placeholder="初始剩余额度" name="input" v-model="card.remainQuota"></input>
			</view>
			
			<view class="flex padding">
				<view class="flex-sub bg-blue padding-sm margin-xs radius text-center" @click="submit">确定</view>
				<view class="flex-sub bg-blue padding-sm margin-xs radius text-center">取消</view>
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
					bank: '0',
					fixedQuota: '',
					billDay: '1',
					dueDay: '1',
					remainQuota: ''
				},
				days: [1,2,3,4,5,6,7,8,9,10],
				banks: ["中国银行", "光大银行", "交通银行", "中信银行", "招商银行", "平安银行"]
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
			},
			billDateChange(e) {
				this.card.billDay = e.detail.value
			},
			dueDateChange(e) {
				this.card.dueDay = e.detail.value
			},
			bankChange(e) {
				this.card.bank = e.detail.value
			}
		}
	}
</script>

<style>
	.uni-form-item .title {
		padding: 20rpx 0;
	}
</style>
