<template>
	<view>
		<swiper :autoplay="true" :circular="true" class="swiper-main">
			<swiper-item v-for="(item,index) in swipers" :key="index">
				<image class="swiper" :src="item.imageUrl" mode="aspectFit"></image>
			</swiper-item>
		</swiper>
		<view class="font-main" style="margin-bottom: 0;margin-top: 5rpx;">
			<text>热门课程</text>
		</view>

		<view @click="toCourseDetail(course.id)" class="course" v-for="(course,index) in courseList" :key="index">
			<image class="course-img" :src="course.cover" mode="aspectFit"></image>
			<view class="course-price">
				<text v-if="course.price===0">免费</text>
				<text v-if="course.price!==0">￥{{course.price}}元</text>
			</view>
			<view class="course-title">{{course.title}}</view>
		</view>

		<view class="font-main">
			<text>名师推荐</text>
		</view>

		<view @click="toTeacherDetail(teacher.id)" class="teacher" v-for="(teacher) in teacherList">

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
	import indexData from '../../mock/index.js'


	export default {
		data() {
			return {
				swipers: indexData.banner,
				courseList: indexData.courseList,
				teacherList: indexData.teacherList
			}
		},
		onLoad() {
			this.getSwipers()
		},
		methods: {
			getSwipers() {},
			// 去课程详情页面
			toCourseDetail(id){
				uni.navigateTo({
					url:'../course/courseDetail?id='+id
				})
			},
			toTeacherDetail(id){
				uni.navigateTo({
					url:'../teacher/teacherDetail?id='+id
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.swiper {
		width: 740rpx;
		height: 240rpx;
		border-radius: 15px;
		// box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.1), 0 6px 20px 0 rgba(0, 0, 0, 0.1);
	}

	.swiper-main {
		margin-left: 5rpx;
		height: 250rpx;
		
	}

	.font-main {
		font-size: 50rpx;
		margin-top: 20rpx;
		margin-bottom: 20rpx;
		text-align: center;
	}

	.box {
		width: 160px;
		height: 260px;
		margin-right: 0;
		background-color: #3F536E;
		display: inline-block;
	}

	.course {
		width: 46%;
		border: #00936c 1px solid;
		border-radius: 8px;
		background-color: #20a6b2;
		text-align: center;
		display: inline-block;
		margin-left: 2%;
		margin-top: 30rpx;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
	}

	.course-img {
		width: 96%;
		height: 200rpx;
		border-radius: 14px;
	}

	.course-price {
		color: #ffa4fb;
	}

	.course-title {
		color: #cdfdff;
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
		
		image{
			width: 340rpx;
			border-radius: 15px;
		}
	}

	.teacher-card {
		width: 350rpx;
		height: 480rpx;
		margin-left: 10rpx;
	}
	.teacher-card-level{
		margin-top: 5px;
		font-size: 40rpx;
	}
	.teacher-card-intro{
		margin-top: 5px;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 7;
		overflow: hidden;
	}
</style>
