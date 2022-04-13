<template>
	<view>
		<view class="font-main">
			名师列表
		</view>

		<view @click="toTeacherDetail(teacher.id)" class="teacher" v-for="(teacher) in teacherList.slice(0,num)">

			<view class="teacher-img">
				<image :src="teacher.avatar" mode="aspectFit"></image>
			</view>

			<view class="teacher-card">
				<view style="margin-top: 6px;"><text style="font-size: 40rpx;">姓名:</text>{{teacher.name}}</view>
				<view class="teacher-card-level">职称:{{teacher.career}}</view>
				<view class="teacher-card-intro"><text style="font-size: 40rpx;">简介:</text>{{teacher.intro}}</view>
			</view>

		</view>
	</view>
</template>

<script>
	import teacherData from '../../mock/teacher.js'
	export default {
		data() {
			return {
				teacherList: teacherData.teacherList,
				num: 3
			}
		},
		methods: {
			toTeacherDetail(id){
				uni.navigateTo({
					url:'teacherDetail?id='+id
				})
			}
		},
		onLoad() {

		},
		onReachBottom() {
			if (this.num > this.teacherList.length) {
				uni.showToast({
					title: '到底啦',
					duration: 1000,
					position:'bottom'
				});
				console.log('到底啦');
			} else {
				console.log('num值==>', this.num);
				console.log('列表长度', this.teacherList.length);
				uni.showLoading({
					title: '加载中'
				});

				setTimeout(() => {
					uni.hideLoading();
					this.num += 3
				}, 500);
			}


		}
	}
</script>

<style lang="scss" scoped>
	.font-main {
		font-size: 40rpx;
		text-align: center;
		margin: 15px;
	}

	.teacher {
		margin: 0 auto;
		padding: 5px;
		width: 700rpx;
		height: 240px;
		margin-bottom: 30px;
		border-radius: 6px;
		display: flex;
		background-color: #64ca95;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.5), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
	}

	.teacher-img {
		margin-top: 0;
		width: 350rpx;
		height: 480rpx;

		image {
			width: 340rpx;
			border-radius: 15px;
		}
	}

	.teacher-card {
		width: 350rpx;
		height: 480rpx;
		margin-left: 10rpx;
	}

	.teacher-card-level {
		margin-top: 5px;
		font-size: 40rpx;
	}

	.teacher-card-intro {
		margin-top: 5px;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 7;
		overflow: hidden;
	}
</style>
