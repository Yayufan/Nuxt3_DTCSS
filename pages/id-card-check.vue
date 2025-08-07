<template>
    <main class="main-section">
        <el-card class="registration-success-card" shadow="hover">
            <p>醫師不需填寫此問卷及簽退,可直接離開會場</p>
            <p><b>護理人員請填入收到的與會Qrcode的信箱進行問卷填寫</b></p>
            <el-form ref="formRef" :model="formData" label-width="120px" class="el-form" label-position="top">
                <el-form-item label="請輸入電子信箱" prop="email" :rules="formRulesTW.email" :show-message="true">
                    <el-input v-model="formData.email" placeholder="請輸入電子信箱"></el-input>
                </el-form-item>

                <el-form-item label="請再次輸入電子信箱" prop="confirmEmail" :rules="confirmEmailRule" :show-message="true">
                    <el-input v-model="formData.confirmEmail" placeholder="請再次輸入電子信箱"></el-input>
                </el-form-item>
                <el-form-item :model="formData" prop="idCard" label="身分證字號:" :rules="formRulesTW.idCard"
                    :show-message="true">
                    <el-input v-model="formData.idCard" placeholder="請輸入身分證字號"></el-input>
                </el-form-item>
                <el-button type="primary" size="large" @click="handleSubmit(formRef)">確認</el-button>
            </el-form>
        </el-card>
    </main>
</template>
<script lang="ts" setup>
import type { FormInstance, FormItemRule } from 'element-plus'
import { formRulesTW } from '@/utils/validation-rules'
import { useMemberData } from '~/composables/useMember'


const route = useRoute()
const router = useRouter()
const category = route.query.category

const { pageData } = useMemberData()

const formRef = ref<FormInstance>()

const formData = reactive({
    idCard: '',
    email: '',
    confirmEmail: ''
})

const confirmEmailValidation = (rule: any, value: any, callback: any) => {
    if (!value) {
        callback(new Error('請再次輸入電子信箱'))
    } else if (value !== formData.email) {
        callback(new Error('兩次輸入的電子信箱不一致'))
    } else {
        callback()
    }
}

const confirmEmailRule = reactive<FormItemRule[]>([
    { required: true, message: '請再次輸入電子信箱', trigger: 'blur' },
    { type: 'email', message: '請輸入正確的電子信箱格式', trigger: 'blur' },
    { validator: confirmEmailValidation, trigger: 'blur' }
])


const handleSubmit = (formEl: FormInstance | undefined) => {
    console.log(formData)
    if (!formEl) return
    formEl.validate(async (valid) => {
        if (valid) {
            let res = await CSRrequest.post('/questionnaire/id_card', {
                body: formData
            })
            console.log("res: ", res)
            if (res.code === 200) {
                router.push({
                    path: '/questionnaire',
                })
                pageData.value = res.data
            }
        } else {

        }
    })
}

console.log("category為: ", category)


</script>
<style lang="scss" scoped>
.main-section {
    display: flex;
    justify-content: center;
    align-items: center;

    .registration-success-card {
        width: 32rem;
        padding: 20px;
        text-align: center;
        background-color: #f9f9f9;
        border-radius: 8px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);

        :deep(.el-card__body) {
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }

        h1 {
            // color: #71B132;
            font-size: 2rem;
        }

        .img-box {
            margin-bottom: 12px;

            img {
                max-width: 50%;
                aspect-ratio: 1 / 1;
                // height: auto;
            }
        }

        .back-home-link {
            display: inline-block;
            margin-top: 20px;
            color: #409eff;
            text-decoration: none;
            font-weight: bold;

            &:hover {
                text-decoration: underline;
            }
        }
    }
}
</style>