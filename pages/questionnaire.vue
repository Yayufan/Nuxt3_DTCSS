<template>
    <main class="common-section">
        <section class="questionnaire-section">
            <div class="questionnaire-info-box">
                <h1 v-if="pageData?.member?.chineseName">親愛的{{ pageData?.member?.chineseName || '' }}您好：</h1>
                <p>
                    感謝您參加本次研討會，為提供更優質的課程內容與學習體驗，敬請您撥冗填寫本問卷，您的意見將是我們未來改善與規劃的重要依據。
                </p>
            </div>

            <div class="questionnaire-content-box">
                <el-form class="questionnaire-form" ref="formRef" :model="formData" label-position="top"
                    :rules="formRules" :show-message="false" :hide-required-asterisk="true">
                    <h2>一、基本資料</h2>
                    <el-form-item label="職稱:" prop="jobTitle" class="hide-required-asterisk">
                        <el-radio-group v-model="formData.jobTitle">
                            <!-- <el-radio label="醫師" value="醫師"></el-radio> -->
                            <el-radio label="護理師" value="護理師"></el-radio>
                            <el-radio label="衛教師" value="衛教師"></el-radio>
                            <el-radio label="其他" value="其他">其他 <el-input :disabled="formData.jobTitle !== '其他'"
                                    v-model="formData.otherJobTitle"></el-input></el-radio>
                        </el-radio-group>
                    </el-form-item>

                    <el-form-item label="任職單位類型:" prop="affiliation" class="hide-required-asterisk">
                        <el-radio-group v-model="formData.affiliation" :min="1" :max="1">
                            <el-radio label="醫學中心" value="醫學中心"></el-radio>
                            <el-radio label="區域醫院" value="區域醫院"></el-radio>
                            <el-radio label="地區醫院" value="地區醫院"></el-radio>
                            <el-radio label="診所" value="診所"></el-radio>
                            <el-radio label="其他" value="其他">其他 <el-input v-model="formData.otherAffiliation"
                                    :disabled="formData.affiliation !== '其他'"></el-input></el-radio>
                        </el-radio-group>
                    </el-form-item>

                    <h2>二、研討會內容評價（請以 1~5 分評分，5 分為非常同意）</h2>
                    <el-form-item>
                        <template #label>
                            <div class="rating-label">
                                <span>題項</span>
                                <div class="rating-scale-pc">
                                    <span>1</span>
                                    <span>2</span>
                                    <span>3</span>
                                    <span>4</span>
                                    <span>5</span>
                                </div>
                            </div>
                        </template>
                        <el-form-item class="inner-form-item" prop="courseContent">
                            <template #label>
                                <div class="rating-label hide-required-asterisk">
                                    <span>1. 課程內容切合實務需求</span>
                                    <el-radio-group v-model="formData.courseContent" class="rating-scale-pc">
                                        <el-radio value="1"></el-radio>
                                        <el-radio value="2"></el-radio>
                                        <el-radio value="3"></el-radio>
                                        <el-radio value="4"></el-radio>
                                        <el-radio value="5"></el-radio>
                                    </el-radio-group>
                                </div>
                            </template>
                            <el-radio-group v-model="formData.courseContent" class="rating-scale-mobile">
                                <el-radio value="1" label="1"></el-radio>
                                <el-radio value="2" label="2"></el-radio>
                                <el-radio value="3" label="3"></el-radio>
                                <el-radio value="4" label="4"></el-radio>
                                <el-radio value="5" label="5"></el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item class="inner-form-item" prop="teachingMethod">
                            <template #label>
                                <div class="rating-label hide-required-asterisk">
                                    <span>2. 講師教學方式清楚易懂</span>
                                    <el-radio-group v-model="formData.teachingMethod" class="rating-scale-pc">
                                        <el-radio value="1"></el-radio>
                                        <el-radio value="2"></el-radio>
                                        <el-radio value="3"></el-radio>
                                        <el-radio value="4"></el-radio>
                                        <el-radio value="5"></el-radio>
                                    </el-radio-group>
                                </div>
                            </template>
                            <el-radio-group v-model="formData.teachingMethod" class="rating-scale-mobile">
                                <el-radio value="1" label="1"></el-radio>
                                <el-radio value="2" label="2"></el-radio>
                                <el-radio value="3" label="3"></el-radio>
                                <el-radio value="4" label="4"></el-radio>
                                <el-radio value="5" label="5"></el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item class="inner-form-item" prop="speakerKnowledge">
                            <template #label>
                                <div class="rating-label hide-required-asterisk">
                                    <span>3. 講師具備專業知識與實務經驗</span>
                                    <el-radio-group v-model="formData.speakerKnowledge" class="rating-scale-pc">
                                        <el-radio value="1"></el-radio>
                                        <el-radio value="2"></el-radio>
                                        <el-radio value="3"></el-radio>
                                        <el-radio value="4"></el-radio>
                                        <el-radio value="5"></el-radio>
                                    </el-radio-group>
                                </div>
                            </template>
                            <el-radio-group v-model="formData.speakerKnowledge" class="rating-scale-mobile">
                                <el-radio value="1" label="1"></el-radio>
                                <el-radio value="2" label="2"></el-radio>
                                <el-radio value="3" label="3"></el-radio>
                                <el-radio value="4" label="4"></el-radio>
                                <el-radio value="5" label="5"></el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item class="inner-form-item" prop="courseTime">
                            <template #label>
                                <div class="rating-label hide-required-asterisk">
                                    <span>4. 課程安排時間適當</span>
                                    <el-radio-group v-model="formData.courseTime" class="rating-scale-pc">
                                        <el-radio value="1"></el-radio>
                                        <el-radio value="2"></el-radio>
                                        <el-radio value="3"></el-radio>
                                        <el-radio value="4"></el-radio>
                                        <el-radio value="5"></el-radio>
                                    </el-radio-group>
                                </div>
                            </template>
                            <el-radio-group v-model="formData.courseTime" class="rating-scale-mobile">
                                <el-radio value="1" label="1"></el-radio>
                                <el-radio value="2" label="2"></el-radio>
                                <el-radio value="3" label="3"></el-radio>
                                <el-radio value="4" label="4"></el-radio>
                                <el-radio value="5" label="5"></el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item class="inner-form-item" prop="site">
                            <template #label>
                                <div class="rating-label hide-required-asterisk">
                                    <span>5. 場地與設備舒適、完善</span>
                                    <el-radio-group v-model="formData.site" class="rating-scale-pc">
                                        <el-radio value="1"></el-radio>
                                        <el-radio value="2"></el-radio>
                                        <el-radio value="3"></el-radio>
                                        <el-radio value="4"></el-radio>
                                        <el-radio value="5"></el-radio>
                                    </el-radio-group>
                                </div>
                            </template>
                            <el-radio-group v-model="formData.site" class="rating-scale-mobile">
                                <el-radio value="1" label="1"></el-radio>
                                <el-radio value="2" label="2"></el-radio>
                                <el-radio value="3" label="3"></el-radio>
                                <el-radio value="4" label="4"></el-radio>
                                <el-radio value="5" label="5"></el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item class="inner-form-item" prop="activityProcess">
                            <template #label>
                                <div class="rating-label hide-required-asterisk">
                                    <span>6. 整體活動流程順暢</span>
                                    <el-radio-group v-model="formData.activityProcess" class="rating-scale-pc">
                                        <el-radio value="1"></el-radio>
                                        <el-radio value="2"></el-radio>
                                        <el-radio value="3"></el-radio>
                                        <el-radio value="4"></el-radio>
                                        <el-radio value="5"></el-radio>
                                    </el-radio-group>
                                </div>
                            </template>
                            <el-radio-group v-model="formData.activityProcess" class="rating-scale-mobile">
                                <el-radio value="1" label="1"></el-radio>
                                <el-radio value="2" label="2"></el-radio>
                                <el-radio value="3" label="3"></el-radio>
                                <el-radio value="4" label="4"></el-radio>
                                <el-radio value="5" label="5"></el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item class="inner-form-item" prop="entireEvent">
                            <template #label>
                                <div class="rating-label hide-required-asterisk">
                                    <span>7. 對本次研討會整體感到滿意</span>
                                    <el-radio-group v-model="formData.entireEvent" class="rating-scale-pc">
                                        <el-radio value="1"></el-radio>
                                        <el-radio value="2"></el-radio>
                                        <el-radio value="3"></el-radio>
                                        <el-radio value="4"></el-radio>
                                        <el-radio value="5"></el-radio>
                                    </el-radio-group>
                                </div>
                            </template>
                            <el-radio-group v-model="formData.entireEvent" class="rating-scale-mobile ">
                                <el-radio value="1" label="1"></el-radio>
                                <el-radio value="2" label="2"></el-radio>
                                <el-radio value="3" label="3"></el-radio>
                                <el-radio value="4" label="4"></el-radio>
                                <el-radio value="5" label="5"></el-radio>
                            </el-radio-group>
                        </el-form-item>
                    </el-form-item>

                    <div class="expect-box">
                        <el-form-item label="您參加本次研討會的主要期待是？（可複選）" prop="expect" class="hide-required-asterisk">
                            <el-checkbox-group class="checkbox-group" v-model="formData.expect">
                                <el-checkbox label="獲得最新臨床實務知識" value="獲得最新臨床實務知識"></el-checkbox>
                                <el-checkbox label="了解特定主題的處置流程（如：血管通路、感染控制等）"
                                    value="了解特定主題的處置流程（如：血管通路、感染控制等）"></el-checkbox>
                                <el-checkbox label="強化個案管理或衛教技巧" value="強化個案管理或衛教技巧"></el-checkbox>
                                <el-checkbox label="取得繼續教育積分／認證" value="取得繼續教育積分／認證"></el-checkbox>
                                <el-checkbox label="與其他單位同儕交流經驗" value="與其他單位同儕交流經驗"></el-checkbox>
                                <el-checkbox label="探索轉職或進修方向" value="探索轉職或進修方向"></el-checkbox>
                                <el-checkbox label="純粹對主題有興趣" value="純粹對主題有興趣"></el-checkbox>
                            </el-checkbox-group>
                        </el-form-item>
                        <el-form-item class="other-expect-box" prop="otherExpect">
                            <el-checkbox v-model="isOtherExpectDisabled" label="其他 :">
                            </el-checkbox>
                            &nbsp
                            <el-input :disabled="!isOtherExpectDisabled" v-model="formData.otherExpect"></el-input>
                        </el-form-item>
                    </div>

                    <h2>三、開放式問題</h2>
                    <el-form-item label="您最滿意的部分是什麼？" prop="mostSatisfied" class="hide-required-asterisk">
                        <el-input type="textarea" v-model="formData.mostSatisfied" placeholder="請輸入您的意見"></el-input>
                    </el-form-item>

                    <el-form-item label="有哪些部分您覺得可以改進？" prop="improve" class="hide-required-asterisk">
                        <el-input type="textarea" v-model="formData.improve" placeholder="請輸入您的意見"></el-input>
                    </el-form-item>
                    <el-form-item label="您希望未來可以加入哪些主題或課程？" prop="future" class="hide-required-asterisk">
                        <el-input type="textarea" v-model="formData.future" placeholder="請輸入您的意見"></el-input>
                    </el-form-item>

                    <el-form-item>
                        <el-button type="primary" @click="handleSubmitQuestionnaire(formRef)">提交問卷</el-button>
                    </el-form-item>
                </el-form>


            </div>
        </section>
    </main>
</template>
<script setup lang="ts">
import { type FormRules, type FormInstance } from 'element-plus';

const router = useRouter();

const { pageData } = useMemberData();

watch(() => pageData.value, (newValue) => {
    if (!newValue || !newValue.attendeesId) {
        if (process.client) {
            ElMessage.warning('請先完成身分證檢查');
            router.push('/id-card-check');
        }
        // ElMessage.warning('請先完成身分證檢查');
    }
}, { immediate: true });

const formRef = ref<FormInstance>();

interface QuestionnaireInterface {
    attendeesId: string;
    jobTitle: string;
    otherJobTitle: string;
    affiliation: string;
    otherAffiliation: string;
    courseContent: string;
    teachingMethod: string;
    speakerKnowledge: string;
    courseTime: string;
    site: string;
    activityProcess: string;
    entireEvent: string;
    expect: string[];
    otherExpect: string;
    mostSatisfied: string;
    improve: string;
    future: string;
}

const formData = reactive<QuestionnaireInterface>({
    attendeesId: '',
    jobTitle: '醫師',
    otherJobTitle: '',
    affiliation: '醫學中心',
    otherAffiliation: '',
    courseContent: '',
    teachingMethod: '',
    speakerKnowledge: '',
    courseTime: '',
    site: '',
    activityProcess: '',
    entireEvent: '',
    expect: [],
    otherExpect: '',
    mostSatisfied: '',
    improve: '',
    future: ''
} as QuestionnaireInterface);

const isOtherExpectDisabled = ref<boolean>(false);



const jobTitleCheck = (rule: any, value: any, callback: any) => {
    if (!value) {
        callback(new Error('請選擇職稱'));
    }
    if (value === '其他' && !formData.otherJobTitle) {
        callback(new Error('請填寫其他職稱'));
    }
    callback();
}

const affiliationCheck = (rule: any, value: any, callback: any) => {
    if (!value) {
        callback(new Error('請選擇任職單位類型'));
    }
    if (value === '其他' && !formData.otherAffiliation) {
        callback(new Error('請填寫其他任職單位類型'));
    }
    callback();
}

const expectCheck = (rule: any, value: any, callback: any) => {
    if (!value || value.length === 0) {
        callback(new Error('請選擇您參加本次研討會的主要期待'));
    }
    if (isOtherExpectDisabled.value && !formData.otherExpect) {
        callback(new Error('請填寫其他期待'));
    }
    callback();
}

const otherExpectCheck = (rule: any, value: any, callback: any) => {
    if (isOtherExpectDisabled.value && !value) {
        callback(new Error('請填寫其他期待'));
    }
    callback();
}

const formRules = reactive<FormRules>({
    jobTitle: [
        { required: true, validator: jobTitleCheck, trigger: 'blur' }
    ],
    affiliation: [
        { required: true, validator: affiliationCheck, trigger: 'blur' }
    ],
    courseContent: [
        { required: true, message: '請評價課程內容符合您的需求', trigger: 'change' }
    ],
    teachingMethod: [
        { required: true, message: '請評價講師教學方式清楚易懂', trigger: 'change' }
    ],
    speakerKnowledge: [
        { required: true, message: '請評價講師具備專業知識與實務經驗', trigger: 'change' }
    ],
    courseTime: [
        { required: true, message: '請評價課程安排時間適當', trigger: 'change' }
    ],
    site: [
        { required: true, message: '請評價場地與設備舒適、完善', trigger: 'change' }
    ],
    activityProcess: [
        { required: true, message: '請評價整體活動流程順暢', trigger: 'change' }
    ],
    entireEvent: [
        { required: true, message: '請評價對本次研討會整體感到滿意', trigger: 'change' }
    ],
    expect: [
        { required: true, validator: expectCheck, trigger: 'blur' }
    ],
    otherExpect: [
        { required: isOtherExpectDisabled.value, validator: otherExpectCheck, trigger: 'blur' }
    ],
    mostSatisfied: [
        { required: true, message: '請輸入您最滿意的部分', trigger: 'blur' }
    ],
    improve: [
        { required: true, message: '請輸入有哪些部分您覺得可以改進', trigger: 'blur' }
    ],
    future: [
        { required: true, message: '請輸入您希望未來可以加入哪些主題或課程', trigger: 'blur' }
    ]
})


watch(() => formData.expect, () => {
    console.log('期望值變更:', formData.expect);
    formData.expect.includes('其他') ? isOtherExpectDisabled.value = true : isOtherExpectDisabled.value = false;
})

const handleSubmitQuestionnaire = (formEl: FormInstance | undefined) => {
    if (!formEl) return;


    formEl.validate(async (valid) => {
        if (valid) {
            formData.attendeesId = pageData.value.attendeesId;

            if (formData.jobTitle === '其他') {
                formData.jobTitle = formData.otherJobTitle === '' ? '其他' : formData.otherJobTitle;
            }

            if (formData.affiliation === '其他') {
                formData.affiliation = formData.otherAffiliation === '' ? '其他' : formData.otherAffiliation;
            }

            if (isOtherExpectDisabled.value) {
                formData.expect.push(formData.otherExpect);
            }
            // submitQuestionnaire(formData);
            let res = await CSRrequest.post('/questionnaire', {
                body: formData
            });

            if (res.code === 200) {
                ElMessage.success('問卷提交成功！');
                // 重置表單
                formEl.resetFields();
                // 跳轉到成功頁面或其他操作
                router.push('/questionnaire-success');
            } else {
                ElMessage.error('問卷提交失敗，請稍後再試');
            }
        } else {
            console.log('表單驗證失敗');
            ElMessage.error('請填寫所有必填項目');
            return false;
        }
    });


    console.log('提交問卷', formData);
};


</script>
<style scoped lang="scss">
.common-section {
    font-family: $common-section-font-family;
    min-height: 60vw;

    // 問卷外框
    .questionnaire-section {
        width: 80%;
        margin: 0 auto;
        padding: 20px;
        background-color: #f9f9f9;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }

    // 問卷內容
    .questionnaire-content-box {
        margin-top: 20px;
        padding: 10px;

        .questionnaire-form {

            .hide-required-asterisk {
                position: relative;

                &:after {
                    content: '*';
                    position: absolute;
                    top: 2px;
                    left: -10px;
                    color: red;
                }
            }

            // 評分標籤
            .rating-label {
                display: flex;
                justify-content: space-between;
                align-items: center;
                margin-bottom: 10px;

                @media screen and (max-width: 550px) {
                    flex-direction: column;
                    align-items: flex-start;

                }

                // 電腦版評分小標題
                .rating-scale-pc {
                    display: flex;
                    gap: 10px;

                    @media screen and (max-width: 550px) {
                        display: none;
                    }

                    span {
                        width: 30px;
                        text-align: center;
                        font-weight: bold;
                    }
                }
            }

            // 評分項目
            :deep(.inner-form-item) {
                display: flex;
                justify-content: space-between;
                width: 100%;

                @media screen and (max-width: 550px) {
                    flex-direction: column;
                    align-items: flex-start;

                }

                .el-form-item__label {
                    width: 100%;
                }

                // 電腦版評分選項
                .rating-label {
                    display: flex;
                    justify-content: space-between;
                    align-items: center;
                    width: 100%;

                    @media screen and (max-width: 550px) {
                        flex-direction: column;
                        align-items: flex-start;
                        padding-left: 8px;
                    }

                    .rating-scale-pc {
                        gap: 18px;

                        @media screen and (max-width: 550px) {
                            display: none;
                        }
                    }

                    .el-radio {
                        margin: 0;
                    }

                }

                // 手機版評分選項
                .rating-scale-mobile {
                    display: none;
                    gap: 10px;

                    @media screen and (max-width: 550px) {
                        display: flex;
                        flex-direction: row;
                        padding-left: 1rem;
                    }

                    .el-radio {
                        width: 30px;
                        margin: 0;
                        text-align: center;
                        font-weight: bold;
                    }
                }
            }

            .expect-box {
                .el-form-item {
                    margin: 0;
                }

                .checkbox-group {
                    display: flex;
                    flex-wrap: wrap;
                    gap: 10px;

                    .el-checkbox {
                        margin-bottom: 10px;
                        text-wrap: wrap;
                    }
                }

                .other-expect-box {
                    display: flex;
                    align-items: center;
                    gap: 10px;
                    margin-bottom: 20px;

                    .el-checkbox {
                        margin-right: 0;
                    }

                    .el-input {
                        width: 100%;
                        max-width: 300px;
                    }
                }
            }
        }
    }
}
</style>

<!-- 親愛的學員您好： 
感謝您參加本次研討會，為提供更優質的課程內容與學習體驗，敬請您撥冗填寫本問卷，您的意見將是我們未來改善與規劃的重要依據。 
一、基本資料 
職稱： 
☐ 醫師☐ 護理師 ☐ 衛教師 ☐ 學生 ☐ 其他：_________ 
任職單位類型： 
☐ 醫學中心 ☐ 區域醫院 ☐ 地區醫院 ☐ 診所 ☐ 其他：_________ 
二、研討會內容評價（請以 1~5 分評分，5 分為非常同意） 
題項	                1	2	3	4	5 
1. 課程內容切合實務需求	☐	☐	☐	☐	☐ 
2. 講師教學方式清楚易懂	☐	☐	☐	☐	☐ 
3. 講師具備專業知識與實務經驗	☐	☐	☐	☐	☐ 
4. 課程安排時間適當	☐	☐	☐	☐	☐ 
5. 場地與設備舒適、完善	☐	☐	☐	☐	☐ 
6. 整體活動流程順暢	☐	☐	☐	☐	☐ 
7. 對本次研討會整體感到滿意	☐	☐	☐	☐	☐ 
您參加本次研討會的主要期待是？（可複選） 
☐ 獲得最新臨床實務知識 
☐ 了解特定主題的處置流程（如：血管通路、感染控制等） 
☐ 強化個案管理或衛教技巧 
☐ 取得繼續教育積分／認證 
☐ 與其他單位同儕交流經驗 
☐ 探索轉職或進修方向 
☐ 純粹對主題有興趣 
☐ 其他：__________ 
三、開放式問題 
您最滿意的部分是什麼？ 
___________________________________________________ 
有哪些部分您覺得可以改進？ 
__________________________________________________ 
您希望未來可以加入哪些主題或課程？ 
___________________________________________________  -->