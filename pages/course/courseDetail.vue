<template>
	<view>
		<view class="course">
			<image class="course-img" :src="courseInfo.cover" mode="aspectFit"></image>
			<view class="course-title">
				<text>{{courseInfo.title}}</text>
			</view>
			<view class="course-price">
				<text v-if="courseInfo.price===0">免费</text>
				<text v-else>价格￥{{courseInfo.price}}元</text>
			</view>
			<view class="course-info">
				<view class="course-info-item">
					浏览量<view class="course-info-item-font">{{courseInfo.viewCount}}</view>
				</view>
				
				<view class="course-info-item">
					销量<view class="course-info-item-font">{{courseInfo.buyCount}}</view>
				</view>
				
				<view class="course-info-item">
					章节数<view class="course-info-item-font">{{courseInfo.lessonNum}}</view>
				</view>
			</view>
			<view class="course-category">
				<view class="course-category-font1">所属分类:</view> 
				<view class="course-category-font2">{{subjectInfo.oneSubjectTitle}}/{{subjectInfo.twoSubjectTitle}}</view>
			</view>
			<!-- 授课教师 -->
			<view class="teacher-title">
				授课教师
			</view>
			<view @click="toTeacherDetail(teacher.id)" class="teacher">
			
				<view class="teacher-img">
					<image :src="teacher.avatar" mode="aspectFit"></image>
				</view>
			
				<view class="teacher-card">
					<view style="margin-top: 6px;"><text style="font-size: 40rpx;">姓名:</text>{{teacher.name}}</view>
					<view class="teacher-card-level">职称:{{teacher.career}}</view>
					<view class="teacher-card-intro"><text style="font-size: 40rpx;">简介:</text>{{teacher.intro}}</view>
				</view>
			
			</view>
			<view style="margin-top: 80rpx; border: #007AFF 1rpx solid;"></view>
		</view>
	</view>
</template>

<script>
	import courseData from '../../mock/course.js'
	import subjectData from '../../mock/subject.js'
	import teacherData from '../../mock/teacher.js'
	export default {
		data() {
			return {
				courseInfo:'',
				subjectInfo:{
					oneSubjectTitle:'',
					twoSubjectTitle:''
				},
				teacher:''
			}
		},
		methods:{
			toTeacherDetail(id){
				uni.navigateTo({
					url:'../teacher/teacherDetail?id='+id
				})
			}
		},
		onLoad(data) {
			// console.log('课程id:', data.id);
			for (let i = 0; i < courseData.courseList.length; i++) {
				if(courseData.courseList[i].id===data.id){
					this.courseInfo = courseData.courseList[i]
				}
			}
			let twoSubjectList=[]
			for (let i = 0; i < subjectData.subjectList.length; i++) {
				if(subjectData.subjectList[i].id===this.courseInfo.subjectParentId){
					this.subjectInfo.oneSubjectTitle = subjectData.subjectList[i].title
					twoSubjectList=subjectData.subjectList[i].children
				}
			}
			for (let i = 0; i < twoSubjectList.length; i++) {
				if(twoSubjectList[i].id===this.courseInfo.subjectId){
					this.subjectInfo.twoSubjectTitle = twoSubjectList[i].title
				}
			}
			
			for (let i = 0; i < teacherData.teacherList.length; i++) {
				if(teacherData.teacherList[i].id===this.courseInfo.teacherId){
					this.teacher = teacherData.teacherList[i]
				}
			}
			// console.log('this.subjectInfo',this.subjectInfo);
		}
	}
</script>

<style lang="scss" scoped>
	.course {
		// margin-top: 200rpx;
		width: 95%;
		margin: 0 auto;
		// border: #007AFF 1px solid;
		background-color: #55aa7f;
		border-radius: 18rpx;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.5), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
		.course-img{
			margin-top: 10rpx;
			// margin: 10rpx auto;
			width: 710rpx;
			height: 400rpx;
			border-radius: 25rpx;
			box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.4);
		}
	}
	.course-title{
		margin-top: 20rpx;
		// border: #007AFF 1px solid;
		text-align: center;
		text-shadow: 2px 2px 5px #426430;
		font-size: 40rpx;
	}
	.course-price{
		margin-top: 20rpx;
		font-size: 40rpx;
		margin-left: 50rpx;
	}
	.course-info{
		margin-top: 40rpx;
		display: flex;
		width: 98%;
		margin: 0 auto;
		justify-content: center;
		// border: #007AFF 1px solid;
		background-color: #00aa7f;
		border-radius: 15rpx;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.5), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
	}
	.course-info-item{
		// border: #007AFF 1px solid;
		font-size: 40rpx;
		margin: 10rpx 60rpx;
		text-align: center;
	}
	.course-category{
		margin-top: 30rpx;
		// border: #007AFF 1px solid;
		font-size: 50rpx;
		display: flex;
		height: 80rpx;
		width: 98%;
		margin-left: 1%;
		border-radius: 15rpx;
		// text-align: center;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.4);
	}
	.course-category-font1{
		// font-style: none;
	}
	.course-category-font2{
		margin-left: 60rpx;
	}
	
	
	.teacher {
		margin-top: 80rpx;
		// margin: 0 auto;
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
	.teacher-title{
		margin: 0 auto;
		margin-top: 50rpx;
		font-size: 60rpx;
		text-align: center;
		// border: #007AFF 1px solid;
		border-radius: 15rpx;
		width: 97%;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.4);
	}
</style>
