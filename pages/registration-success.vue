<template>
    <main class="main-section">
        <el-card class="registration-success-card" shadow="hover">
            <div class="img-box">
                <img src="/assets/img/check.png" alt="">
            </div>
            <h1>會員註冊報名成功！</h1>
            <p>請至電子信箱確認您的報名資訊。</p>
            <p>護理師繳費連結請至信箱查看，24小時內未付款完成請重新註冊</p>
            <p>如有任何問題，請聯繫 joanne.wang@zhongfu-pr.com.tw</p>
            <nuxt-link to="/" class="back-home-link">返回首頁</nuxt-link>
        </el-card>
    </main>
</template>
<script lang="ts" setup>
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

        h1 {
            color: #71B132;
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