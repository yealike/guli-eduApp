<template>
	<view>
		<view class="teacher">
			<view class="teacher-img">
				<image :src="teacherInfo.avatar" mode="aspectFit"></image>
			</view>

			<view class="teacher-card">
				<view style="margin-top: 6px;"><text style="font-size: 40rpx;">姓名:</text>{{teacherInfo.name}}</view>
				<view class="teacher-card-level">职称:{{teacherInfo.career}}</view>
				<view class="teacher-card-intro"><text style="font-size: 40rpx;">简介:</text>{{teacherInfo.intro}}</view>
			</view>
		</view>
		<!-- 讲师简介 -->
		<view class="title">
			讲师简介
		</view>
		<view class="intro">
			{{teacherInfo.intro}}
		</view>
		<view class="title">
			教授课程
		</view>

		<!-- 课程列表展示 -->
		<view @click="toCourseDetail(course.id)" class="course" v-for="(course,index) in courseList" :key="index">
			<image class="course-img" :src="course.cover" mode="aspectFit"></image>
			<view class="course-price">
				<text v-if="course.price===0">免费</text>
				<text v-if="course.price!==0">￥{{course.price}}元</text>
			</view>
			<view class="course-title">{{course.title}}</view>
		</view>
		<view style="margin-bottom: 30rpx; height: 40rpx;"></view>
	</view>
</template>

<script>
	import teacherData from '../../mock/teacher.js'
	import courseData from '../../mock/course.js'
	export default {
		data() {
			return {
				teacherInfo: '',
				courseList: [],
				teacherId: ''
			}
		},
		methods: {
			// 去课程详情页面
			toCourseDetail(id) {
				uni.navigateTo({
					url: '../course/courseDetail?id=' + id
				})
			}
		},
		onLoad(data) {
			console.log('讲师id==>', data.id);
			this.teacherId = data.id
			for (let i = 0; i < teacherData.teacherList.length; i++) {
				if (this.teacherId === teacherData.teacherList[i].id) {
					this.teacherInfo = teacherData.teacherList[i]
				}
			}

			let count = 0;
			for (let i = 0; i < courseData.courseList.length; i++) {
				if (this.teacherId === courseData.courseList[i].teacherId) {
					this.courseList[count++] = courseData.courseList[i]
				}
			}
			console.log('课程列表==>', this.courseList);
		}
	}
</script>

<style lang="scss" scoped>
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

	.title {
		text-align: center;
		font-size: 60rpx;
		text-shadow: 2px 2px 5px #426430;
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
	
	.intro{
		width: 98%;
		margin: 0 auto;
		padding: 5rpx;
		font-size: 40rpx;
		margin-top: 40rpx;
		margin-bottom: 40rpx;
		border-radius: 15rpx;
		background-color: #64ca95;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.5), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
	}
</style>
