<template>
    <main class="common-section">

        <div class="main-section">
            <div class="content">
                <div class="conference-info-box">
                    <h1 class="topic">「血管通路 我來守護」</h1>
                    <h1 class="topic">第十三屆血液透析瘻管治療與照護研討會</h1>
                    <p>活動日期 : 09/06 (六) – 09/07 (日)</p>
                    <p>活動時間 : 09/06 (六) 08:30-17:00 ; 09/07 (日) 08:30-12:00 ​</p>
                    <p>活動地點 : 大林慈濟醫院 大愛樓 5F大講堂 (嘉義縣大林鎮民生路2號)</p>
                    <!-- <div class="btn-box">
                        <el-button class="agenda-download-btn" type="primary" size="large">議程表</el-button>
                        <el-button class="add-calendar-btn" type="primary" size="large">
                            <el-icon><ElIconCalendar /></el-icon><span>加入行事曆</span>
                        </el-button>

                    </div> -->
                </div>
                <div class="conference-registration-box">
                    <el-form class="registration-form" :model="formData" ref="registrationForm" label-position="top">
                        <el-form-item label="報名分類" prop="category" :rules="formRulesTW.category">
                            <el-radio-group v-model="formData.category">
                                <el-radio value="8">9/6 醫師手術直播研討會</el-radio>
                                <el-radio value="9">9/7 護理人員研討會</el-radio>
                                <el-radio value="10">9/7 護理人員研討會_慈濟體系專區</el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <div class="form-section">
                            <div class="left-section">

                                <el-form-item v-if="formData.category === '8'" prop="country" label="國家" :rules="formRulesTW.country">
                                    <el-select v-model="formData.country" filterable placeholder="請選擇國家">
                                        <el-option v-for="item in country" :key="item" :label="item"
                                            :value="item"></el-option>
                                    </el-select>
                                </el-form-item>

                                <el-form-item :label="formData.category === '8'? '中文姓名' : '中文姓名(申請學分用)'" prop="chineseName" :rules="formRulesTW.chineseName">
                                    <el-input v-model="formData.chineseName" placeholder="請輸入中文姓名"></el-input>
                                </el-form-item>

                                <el-form-item v-if="formData.category !== '8'" label="身分證字號(申請學分用)" prop="idCard"
                                    :rules="formRulesTW.idCard">
                                    <el-input v-model="formData.idCard" placeholder="請輸入身分證字號"></el-input>
                                </el-form-item>

                                <el-form-item label="電子信箱(僅能報名一位)" prop="email" :rules="formRulesTW.email">
                                    <el-input v-model="formData.email" placeholder="請輸入電子信箱"></el-input>
                                </el-form-item>

                                <el-form-item label="電子信箱驗證" prop="confirmEmail" :rules="confirmEmailRule">
                                    <el-input v-model="formData.confirmEmail" placeholder="請再次輸入電子信箱"></el-input>
                                </el-form-item>
                                <el-form-item label="聯絡電話" prop="phone" :rules="formRulesTW.phone">
                                    <el-input v-model="formData.phone" placeholder="請輸入聯絡電話"></el-input>
                                </el-form-item>
                            </div>

                            <div class="right-section">

                                <el-form-item label="所屬科部" prop="affiliation" :rules="formRulesTW.affiliation">
                                    <el-input v-model="formData.affiliation" placeholder="請輸入所屬單位"></el-input>
                                </el-form-item>

                                <el-form-item label="職稱" prop="jobTitle" :rules="formRulesTW.jobTitle">
                                    <el-input v-model="formData.jobTitle" placeholder="請輸入職稱"></el-input>
                                </el-form-item>

                                <el-form-item v-if="formData.category === '8'" label="醫院" prop="receipt" :rules="formRulesTW.receipt">
                                    <el-input v-model="formData.receipt" placeholder="請輸入醫院名稱"></el-input>
                                </el-form-item>

                                <el-form-item v-if="formData.category !== '8'" label="醫院全稱(收據抬頭，如未需要請填 '無') " prop="receipt" :rules="formRulesTW.receipt">
                                    <el-input v-model="formData.receipt" placeholder="請輸入醫院全稱"></el-input>
                                </el-form-item>

                                <el-form-item label="驗證碼" prop="verificationCode" :rules="formRulesTW.verificationCode">
                                    <div class="captcha-container">
                                        <el-input v-model="formData.verificationCode" placeholder="請輸入驗證碼"></el-input>
                                        <img :src="captcha.image" alt="captcha" @click="getCaptcha">
                                    </div>
                                </el-form-item>
                            </div>
                        </div>



                        <p v-if="formData.category === '8'">※ 本活動提供素食午膳</p>
                        <p v-if="formData.category === '9'">※ 本活動不提供退費</p>

                        <div class="reminder">
                            <p>個人資料蒐集、處理及利用告知暨同意書
                                為完成本活動之報名與後續聯繫事宜，主辦單位將蒐集您於本表單中所提供之個人資料（包括但不限於姓名、聯絡方式、電子郵件等）。</p>
                            <p>
                                您的個人資料將僅限於本活動相關之報名確認、通知、活動資訊提供及後續聯繫用途，並依《個人資料保護法》及相關法令規定予以保護。
                                除非經您另行同意或法律另有規定，您的個人資料不會提供給第三方或作為其他用途使用。</p>
                            <p>
                                您有權查詢、更正、請求刪除或停止使用您的個人資料。若您不同意提供個人資料，可能影響報名及相關通知之權益。 請您詳閱以上說明並確認同意後，再提交本表單。</p>
                        </div>

                        <el-form-item>
                            <el-button class="submit-btn" type="primary"
                                @click="handleSubmit(registrationForm)">確認送出</el-button>
                        </el-form-item>
                    </el-form>

                    <!-- <el-button @click="router.push('/registration-success')">test</el-button> -->
                </div>
            </div>

        </div>

    </main>
</template>
<script lang="ts" setup>
import type { FormInstance } from 'element-plus';
import { formRulesTW } from '@/utils/checkSum';
import countryJson from '@/assets/data/countries.json';

const country = ref(countryJson);

const getCaptcha = async () => {
    let res = await CSRrequest.get('/member/captcha');
    formData.verificationCode = '';
    console.log('獲取驗證碼', res);
    Object.assign(captcha, res.data);
}

const captcha = reactive({
    image: '',
    key: ''
})

const vaildConfirmEmail = (rule: any, value: string, callback: any) => {

    if (!value) {
        callback(new Error("請再次輸入電子信箱"))
    } else if (value !== formData.email) {
        callback(new Error("兩次輸入的電子信箱不一致"))
    } else {
        callback()
    }
}

const confirmEmailRule = [
    { required: true, message: '請再次輸入電子信箱', trigger: 'blur' },
    { validator: vaildConfirmEmail, trigger: 'blur' }
];


const registrationForm = ref<FormInstance>();

const formData = reactive({
    category: '8',
    chineseName: '',
    country: '',
    idCard: '',
    email: '',
    confirmEmail: '',
    phone: '',
    affiliation: '',
    jobTitle: '',
    receipt: '',
    verificationCode: '',
    verificationKey: ''
})
// 送出資料後將立即跳轉至付款頁面，如未完成付款資料將於一天後刪除
const router = useRouter();

const handleSubmit = (formEl: FormInstance | undefined) => {
    if (!formEl) return;

    formEl.validate(async (valid) => {
        if (valid) {
            // 提交表單邏輯
            formData.verificationKey = captcha.key; // 將驗證碼key添加到表單數據中
            if (formData.category === '9') {
                ElMessageBox.confirm(
                    '繳費連結請至信箱查看，24小時內未付款完成請重新註冊',
                    '提示',
                    {
                        confirmButtonText: '確定',
                        cancelButtonText: '取消',
                        type: 'warning'
                    }
                ).then(async () => {
                    // 確認後提交表單
                    let res = await CSRrequest.post('/member', {
                        body: formData
                    });
                    console.log(res)
                    if (res.code === 200) {
                        console.log('提交結果', res);
                        ElMessage.success('報名成功'); formEl.resetFields(); // 重置表單 
                        getCaptcha(); // 重新獲取驗證碼
                        if (res.data) {
                            console.log('重定向到', res.data);
                            router.push('/registration-success');
                            // router.push(res.data);
                        }
                    } else {
                        ElMessage({
                            message: `報名失敗 : ${res.msg}`,
                            type: 'error'
                        }); getCaptcha(); // 重新獲取驗證碼
                        console.error('報名失敗', res);
                    }
                }).catch(() => {
                    console.log('取消報名');
                });
            } else {
                let res = await CSRrequest.post('/member', {
                    body: formData
                });
                console.log(res);
                if (res.code === 200) {
                    console.log('提交結果', res);
                    ElMessage.success('報名成功'); formEl.resetFields(); // 重置表單
                    getCaptcha(); // 重新獲取驗證碼
                
                    // if (res.data) {
                        // console.log('重定向到', res.data);
                        // router.push(res.data);
                        router.push('/registration-success');
                    // }
                } else {
                    ElMessage({
                        message: `報名失敗 : ${res.msg}`,
                        type: 'error'
                    });
                    getCaptcha(); // 重新獲取驗證碼
                    console.error('報名失敗', res);
                }
            }
        } else {
            console.error('表單驗證失敗');
            ElMessage.error('請檢查表單輸入是否正確');
            getCaptcha(); // 表單驗證失敗時重新獲取驗證碼
            return false;
        }
    });
};

onMounted(() => {
    getCaptcha();
});



</script>
<style lang="scss" scoped>
.common-section {
    font-family: $common-section-font-family;
    min-height: 60vw;

    .content {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 3rem;
        padding: 0 2.5rem;

        @media screen and (max-width: 768px) {
            flex-direction: column;
            align-items: center;
            padding: 0;
        }

        .conference-info-box {
            display: flex;
            flex-direction: column;
            justify-content: center;
            width: 100%;
            padding: 20px;
            text-align: center;


            .topic {
                font-size: 1.5rem;
                font-weight: bold;
                color: #333;
                margin-bottom: 20px;
            }

            .btn-box {
                display: flex;
                justify-content: center;
                gap: 1rem;
                margin-top: 20px;

                .el-button {
                    border-radius: 20px;
                    border: none;
                }

                .agenda-download-btn {
                    background-color:#971B6A;
                    color: white;
                }

                .add-calendar-btn {
                    background-color:#CA7D8F;
                    color: white;
                    display: flex;
                    align-items: center;
                    gap: 0.5rem;
                }


                @media screen and (max-width: 768px) {
                    flex-direction: column;
                    align-items: center;

                    .free {
                        width: 100%;
                        margin-bottom: 10px;
                    }
                }
            }
        }

        .conference-registration-box {
            width: 80%;
            margin: 0 auto;
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);


            .free {
                color: red;
            }

            .registration-form {
                width: 90%;
                margin: 0 auto;
                // font-size: 1rem;

                :deep(.el-form-item__label) {
                    font-size: 1rem;
                    color: #333;
                }

                :deep(.el-input__inner) {
                    font-size: 1rem;
                    color: #333;
                }

                :deep(.el-radio__label) {
                    font-size: 1rem;
                    color: #333;
                }

                :deep(.el-select__inner) {
                    font-size: 1rem;
                    color: #333;
                }

                .form-section {
                    display: flex;
                    gap: 2rem;

                    @media screen and (max-width: 768px) {
                        flex-direction: column;
                        gap: 1rem;

                    }

                    .left-section,
                    .right-section {
                        flex: 1;

                    }
                }
            }

            .reminder {
                font-size: 1rem;
                color: #666;
                margin-top: 20px;
                line-height: 1.5;

                p {
                    margin-bottom: 10px;
                }
            }

            .captcha-container {
                display: flex;
                width: 100%;
                gap: 1rem;

                @media screen and (max-width: 768px) {
                    flex-direction: column;
                    align-items: center;

                }

                el-input {
                    width: 60%;

                    @media screen and (max-width: 768px) {
                        width: 100%;
                    }
                }

                img {
                    cursor: pointer;
                    // width: 30%;

                    @media screen and (max-width: 768px) {
                        // width: 60%;
                    }
                }
            }

            .submit-btn {
                width: 100%;
                margin-top: 20px;
                background-color: #E87B86;
            }
        }

    }

}
</style>