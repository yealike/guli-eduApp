<template>
	<view>
		<view class="pick-main">
			<text class="picked">请选择:</text>
			<picker mode="selector" range-key="title" :range="subjectList" @change="picked">
				<view class="pick-course">
					<text v-if="pickTitle ===''">---课程---</text>
					<text v-if="pickTitle !==''">>{{pickTitle}}<</text>
				</view>
			</picker>
			<button type="default" @click="getAllCourse" hover-class="hover"><text class="pick-btn-tex">全部课程</text></button>
		</view>
		
		<view class="course-mainTitle">
			<text v-if="pickTitle===''">全部课程</text>
			<text v-if="pickTitle!==''">{{pickTitle}}</text>
		</view>
		
		<view @click="toCourseDetail(course.id)" class="course" v-for="(course,index) in courseList">
			<image class="course-img" :src="course.cover" mode="aspectFit"></image>
			<view class="course-price">
				<text v-if="course.price===0">免费</text>
				<text v-if="course.price!==0">￥{{course.price}}元</text>
			</view>
			<view class="course-title">{{course.title}}</view>
		</view>
	</view>
</template>

<script>
	import courseData from '../../mock/course.js'
	import sunjectData from '../../mock/subject.js'
	export default{
		onLoad(options) {
			console.log('接收到的参数==>',options);
			this.subjectId =options.id
			
			let count= 0;
			for (let i = 0; i < courseData.courseList.length; i++) {
				if(this.subjectId===courseData.courseList[i].subjectParentId){
					this.courseList[count++] = courseData.courseList[i]
				}
			}
			this.initCourseList = this.courseList
		},
		data(){
			return{
				courseList: [],
				subjectList:[],
				subjectId:'',
				pickTitle:'',
				initCourseList:[],
				
			}
		},
		methods:{
			// 获取全部课程
			getAllCourse(){
				this.courseList = this.initCourseList
			},
			// 去课程详情页面
			toCourseDetail(id){
				uni.navigateTo({
					url:'./courseDetail?id='+id
				})
			},
			// 切换课程分类
			picked(e){
				let courseList2=[]
				let count=0;
				const subIndex= e.detail.value;
				for (let i = 0; i < courseData.courseList.length; i++) {
					// console.log('courseData.courseList[i]==>',courseData.courseList[i].subjectId);
					if(courseData.courseList[i].subjectId===this.subjectList[subIndex].id){
						// this.courseList[i]=courseData.courseList[i]
						
						courseList2[count++]=courseData.courseList[i]
						
						// console.log('==>',courseData.courseList[i]);
						// this.courseList[i]=courseData.courseList[i]
					}
				}
				// 将课程分类的标题赋值给 pickTitle
				this.pickTitle = this.subjectList[subIndex].title
				// console.log('courseList2=>',courseList2);
				this.courseList = courseList2
			}
		},
		onShow() {
			for (var i = 0; i < sunjectData.subjectList.length; i++) {
				if(sunjectData.subjectList[i].id===this.subjectId){
					// console.log(sunjectData.subjectList[i].children);
					this.subjectList = sunjectData.subjectList[i].children
				}
			}
			
		}
		
	}
</script>

<style lang="scss" scoped>
	.pick-main{
		margin: 15rpx auto;
		background-color: #00aa7f;
		height: 90rpx;
		width: 96%;
		padding-top: 25rpx;
		display: flex;
		border-radius: 10rpx;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
		.picked{
			font-size: 40rpx;
			height: 60rpx;
			width: 150rpx;
			margin-right: 20rpx;
			border-radius: 10rpx;
			margin-left: 30rpx;
			box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
		}
	  .pick-course{
			font-size: 40rpx;
			border: #00aaff 1px solid;
			border-radius: 9rpx;
			box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
		}
		.hover{
			background-color: #a1db92;
		}
		button{
			height: 60rpx;
			width: 180rpx;
			margin-left: 15rpx;
			background-color: #00aa7f;
			position: relative;
			border: #00aa7f 1px solid;
			box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
		}
		.pick-btn-tex{
			margin-top: -4px;
			font-size: 30rpx;
			margin-left: -30px;
			position: absolute;
			text-shadow: 2px 2px 5px #406230;
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
	.course-mainTitle{
		margin: 60rpx 30rpx auto;
		font-size: 60rpx;
		text-align: center;
		width: 93%;
		height: 80rpx;
		border: #00aa7f 1px solid;
		border-radius: 10rpx;
		background-color: #55aa7f;
		text-shadow: 2px 2px 5px #426430;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.6);
	}
</style>
