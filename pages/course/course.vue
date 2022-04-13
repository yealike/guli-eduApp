<template>
	<view>
		<view style="font-size: 40rpx; text-align: center;margin-top: 20px;">课程列表</view>

		<view class="icon" v-for="(sub,index) in subjectList" >
			<view class="icon-front">
				<image @click="showFront(sub.id)" src="../../static/icon/front.png" mode="aspectFit"></image>
				{{sub.title}}
			</view>
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
		<view style="margin-bottom: 30rpx;"></view>
	</view>
</template>

<script>
	import subjectData from '../../mock/subject.js'
	import courseData from '../../mock/course.js'
	export default {
		data() {
			return {
				subjectList: subjectData.subjectList,
				courseList: courseData.courseList
			}
		},
		methods: {
			// 去课程分类页面
			showFront(id){
				console.log('点击...,id=',id);
				uni.navigateTo({
					url:'./courseFront?id='+id
				})
			},
			// 去课程详情页面
			toCourseDetail(id){
				uni.navigateTo({
					url:'./courseDetail?id='+id
				})
			}
		},
		onLoad() {

		}
	}
</script>

<style scoped lang="scss">
	.icon {
		display: inline-block;
		// justify-content: center;

		.icon-front {
			margin-left: 60rpx;
			width: 260rpx;
			text-align: center;
			// border: 1px solid;
		}

		image {
			width: 250rpx;
			height: 100rpx;
		}
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
</style>
