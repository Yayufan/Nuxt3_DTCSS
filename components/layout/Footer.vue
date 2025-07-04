<template>
    <footer class="footer-section">
        <div class="footer-box">
            <p> 「血管通路 我來守護」 第十三屆血液透析瘻管治療與照護研討會
            </p>
            <p>All Rights Reserved©2025</p>
        </div>
    </footer>
</template>
<script lang="ts" setup>
import Title from './Title.vue';
</script>
<style lang="scss" scoped>
.footer-section {
    background-color: #140F4B;
    // background: url('../../assets/img/ticbcs_footer.jpg') no-repeat top center;
    background-size: cover;
    padding: 2rem 0;

    .footer-box {
        display: flex;
        justify-content: space-between;
        // flex-direction: column;
        width: 90%;
        color: white;
        margin: 0 auto;
        font-size: 1.1rem;
        font-weight: bold;

        @media screen and (max-width: 768px) {
            flex-direction: column;
            align-items: center;
            text-align: center;
        }
    }
}
</style>