<template>
    <main class="common-section">
        <div v-html="form" ref="formRef" style="display: none;"></div>
    </main>
</template>

<script lang="ts" setup>
import Banner from '@/components/layout/Banner.vue';
import Breadcrumbs from '@/components/layout/Breadcrumbs.vue';



const router = useRouter();





interface Order {
    itemsSummary: string;
    totalAmount: number;
    status: number;
    ordersId: number;
}


/**----------------------------前往付款------------------- */
const orderId = router.currentRoute.value.query.orderId as string;
console.log('orderId', orderId)
const formRef = ref<any>()

const form = ref<any>()

const getOrders = async () => {

    let res = await CSRrequest.get(`/orders/payment`, {
        params: {
            id: orderId
        }
    })

    console.log(res.code === 500)
    if (res.code === 500) {
        ElMessageBox.confirm(
            '此付款連結已失效，請重新註冊並於獲得付款連結24小時內完成付款',
            '提示',
            {
                confirmButtonText: '確定',
                type: 'warning',
                showCancelButton:false
            }
        ).then(async () => {
            router.push('/');
        }

        ).catch((e) => {
            console.log(e);
        });
    }

    form.value = res.data

    await nextTick();
    if (formRef.value) {
        const formItem = formRef.value.querySelector("form")
        console.log(formItem)
        formItem.submit()
    }



}


onMounted(() => {
    getOrders()
})
</script>

<style lang="scss" scoped>
.common-section {
    font-family: $common-section-font-family;

    .table-section {
        margin-top: 1rem;
        padding: 2rem;
        display: flex;
        justify-content: center;
        align-items: center;
        // background: url('assets/img/topbs_background-image.jpg') no-repeat center center;

        .table-box {
            // width: 80%;
            display: flex;
            flex-direction: column;
            background-color: white;
            border-radius: 15px;
            padding: 1rem;
            justify-content: center;

            .info {
                font-size: 1rem;
                color: red;
                // margin-bottom: 1rem;
            }

            .taiwan {
                td {
                    border-right: 1px white solid;
                }

                .odd {
                    td {
                        &:not(:last-child) {
                            position: relative;

                            &::after {
                                position: absolute;
                                top: 0px;
                                right: -1px;
                                content: '';
                                display: block;
                                width: 1px;
                                height: 100%;
                                background-color: #E8979E;
                                z-index: 10;
                            }
                        }
                    }
                }
            }

            .orders-table {
                overflow: hidden;
                background-color: white;
                font-size: 1.3rem;
                border-collapse: separate;
                border-spacing: 0 0.3rem;
                width: 70vw;

                @media screen and (max-width: 1048px) {
                    font-size: 1rem;
                }

                th {
                    padding: 1rem;
                    border-radius: 15px;
                    text-align: start;
                }

                td {
                    padding: 0.5rem 1rem;
                }

                .header-row {
                    position: relative;

                    &::after {
                        position: absolute;
                        bottom: 5px;
                        right: 0;
                        content: '';
                        display: block;
                        width: 100%;
                        height: 0.1rem;
                        background-color: #CACACA;
                    }
                }

                .first-col {
                    border-top-left-radius: 5px;
                    border-bottom-left-radius: 5px;
                }

                .last-col {
                    border-top-right-radius: 5px;
                    border-bottom-right-radius: 5px;
                    border: none !important;
                }



                .even {
                    td {
                        background-color: #E8979E;
                        color: white;
                        font-weight: bold;
                    }
                }

                .odd {
                    td {
                        background-color: white;
                        color: #E8979E;
                        font-weight: bold;
                    }


                }

                .btn-col {
                    background-color: white;
                    padding: 0.5rem 0.5rem;
                    border-radius: 5px;
                }


                .pay-btn {
                    background-color: #26AE07;
                    color: white;
                    // font-size: 1.3rem;
                    height: 100%;
                    cursor: pointer;
                    padding: 0.5rem 1rem;
                    margin-left: 0.3rem;
                    border-radius: 5px;
                    width: 40%;
                }


                .completed {
                    background-color: #D77102 !important;
                    color: white;
                    text-align: center;
                    border-radius: 5px;
                    cursor: default;

                }

                .temp-col {
                    background-color: white !important;
                    width: 0.1rem;
                    padding: 0;
                    border: none !important;
                }

                .not-pay {
                    text-align: center;
                    background-color: #26AE07 !important;
                    color: white !important;
                    border-radius: 5px;
                    width: 13%;
                    cursor: pointer;

                    &.disabled {
                        background-color: #26AE07 !important;
                        opacity: 0.5;
                        cursor: not-allowed;
                    }
                }

            }
        }

    }


}
</style>