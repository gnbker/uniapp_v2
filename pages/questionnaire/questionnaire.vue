<template>
	<view>
		<image class="questionnaire_icon" mode="widthFix" :src="questionnaire.icon"></image>

		<view class="questionnaire_title">{{questionnaire.title}} </view>
		<view class="question_list">
			<view class="question" v-for="(question, index) in questionnaire.questions">
				<view class="question_title">{{index + 1}}. {{question.title}}</view>
				<radio-group @change="radiochange($event, index)">
					<label class="option_label" v-for="(option, o_index) in question.options" :key="o_index">
						<view>
							<radio :value="option" :checked="option == checklist[index]"></radio>
						</view>
						<view>{{option}}</view>
					</label>
				</radio-group>
			</view>
		</view>
		<button class="submit_btn" type="primary" @click="submit">提交</button>
		<view style="height: 50px;"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				collectionList: "questionnaire",
				questionnaire: {},
				checklist: []
			}
		},
		methods: {
			submit() {
				console.log(this.checklist)
				for (let i = 0; i < this.checklist.length; i++) {
					if (this.checklist[i] == "") {
						uni.showModal({
							title: "问卷未完成",
							content: "请完成问卷后提交",
							showCancel: false
						})
						return
					}
				}
			},
			radiochange(e, index) {
				console.log("e:", e)
				console.log(index)
				this.$set(this.checklist, index, e.detail.value)
			},
			radioGroupChange(evt, index) {
				console.log(evt)
				console.log(index)
				this.questions[index]["selected"] = evt
			},
			test() {
				console.log($env.uid)
			},
			summary() {
				var score = 0;
				for (let i = 0; i < this.questions.length; i++) {
					let question = this.questions[i];
					let right_index = question.right_index;
					console.log(question["selected"], question["options"][0], question["options"][1], question["options"][
						right_index
					])
					if (question["selected"] == null || question["selected"] == "") {
						uni.showModal({
							title: "题目没有完成:",
							content: "请完成所以题目后提交"
						})
						return
					}
					if (question["selected"] == question["options"][right_index]) {
						console.log(true)
						score += 1;
					}
				}
			}
		},
		mounted() {
			const db = uniCloud.database();
			db.collection("questionnaire").get().then(res => {
				console.log(res.result.data)
				this.questionnaire = res.result.data[0]
				var tmplist = []
				for (let i = 0; i < res.result.data[0].questions.length; i++) {
					tmplist[i] = ""
				}
				this.checklist = tmplist
			}).catch(err => {
				console.log(err)
			})
		}
	}
</script>

<style scoped>
	.question {
		margin-bottom: 20px;
	}

	.option_label {
		margin-top: 3px;
		line-height: 18px;
		font-size: 16px;
		margin-bottom: 4px;
	}

	.question_title {
		font-size: 17px;
		line-height: 22px;
		margin-bottom: 10px;
	}

	.question_list {
		width: 90%;
		margin-left: 5%;
	}

	.questionnaire_icon {
		/* position: absolute; */
		/* top: 0; */
		z-index: -99;
		width: 100%;
		height: 30px;
	}

	.questionnaire_title {
		width: 90%;
		margin-left: 5%;
		font-size: 21px;
		margin-top: 2px;
		margin-bottom: 7px;
	}

	.option_label {
		display: flex;
	}

	.submit_btn {
		width: 80%;
		margin-left: 10%;
		margin-top: 30px;
	}
</style>
