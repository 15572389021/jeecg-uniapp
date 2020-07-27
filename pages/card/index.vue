<template name="index">
	<view>
		<cu-custom bgColor="bg-gradual-pink" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">编辑卡片</block>
		</cu-custom>
		<scroll-view>
			<view class="cu-card article" :class="isCard?'no-card':''">
				<view class="cu-item shadow">
					<view class="title"><view class="text-cut">无意者 烈火焚身;以正义的烈火拔出黑暗。我有自己的正义，见证至高的烈火吧。</view></view>
					<view class="content">
						<image src="https://ossweb-img.qq.com/images/lol/web201310/skin/big10006.jpg"
						 mode="aspectFill"></image>
						<view class="desc">
							<view class="text-content"> 折磨生出苦难，苦难又会加剧折磨，凡间这无穷的循环，将有我来终结！真正的恩典因不完整而美丽，因情感而真诚，因脆弱而自由！</view>
							<view>
								<view class="cu-tag bg-red light sm round">正义天使</view>
								<view class="cu-tag bg-green light sm round">史诗</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			<view class="cu-list menu-avatar" >
				<view class="cu-item margin-sm radius margin-bottom-xsl" style="height: 230rpx;border-radius:15rpx;" v-for="card in cardList" :key="card">
					<view class="cu-avatar round lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
						<view class="content">
							<view class="text-grey">凯尔</view>
							<view class="text-gray text-sm flex">
								<view class="text-cut">
									<text class="cuIcon-infofill text-red  margin-right-xs"></text>
									我已天理为凭，踏入这片荒芜，不再受凡人的枷锁遏制。我已天理为凭，踏入这片荒芜，不再受凡人的枷锁遏制。
								</view> </view>
							</view>
						<view class="action">
						<view class="text-grey text-xs">22:20</view>
						<view class="cu-tag round bg-grey sm">5</view>
					</view>
				</view>
			</view>
		</scroll-view>
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
				cardList: [1,2,3,4,5,6,7,8,9]
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
