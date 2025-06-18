<template>
    <div class="common-section">
        <!-- <img src="../assets/img/sponsor_list.png" alt=""> -->
         <Title title="Gallery(2023)"></Title>

        <div class="gallery">
            <div v-for="(group, groupIndex) in groupedImages1" :key="groupIndex" class="image-group">
                <span v-for="(image, imgIndex) in group" :key="imgIndex" class="image-item">
                    <img :src="image" alt="Sponsor Image" />
                </span>
            </div>
        </div>

        <div class="gallery">
            <div v-for="(group, groupIndex) in groupedImages2" :key="groupIndex" class="image-group">
                <span v-for="(image, imgIndex) in group" :key="imgIndex" class="image-item">
                    <img :src="image" alt="Sponsor Image" />
                </span>
            </div>
        </div>




    </div>
</template>
<script lang="ts" setup>
import Title from '@/components/layout/Title.vue';


const cols = ref(6);


const handleResize = () => {
    console.log('handleResize', window.innerWidth);
    if (window.innerWidth < 768) {
        cols.value = 2;
    } else if (window.innerWidth < 1024) {
        cols.value = 3;
    } else {
        cols.value = 6;
    }

    groupImages();
    groupImages2();
};



const groupedImages1 = ref<string[][]>([]);


const groupImages = () => {
    groupedImages1.value = []; // 清空之前的分組
    const modules1 = import.meta.glob('../assets/img/ticbcs_gallery/*.{png,jpg,jpeg,svg}', { eager: true, query: '?url', import: 'default' });

    const galleryImages1 = ref<string[]>(Object.values(modules1) as string[]);
    galleryImages1.value.forEach((image, index) => {
        const groupIndex = Math.floor(index / cols.value);
        if (!groupedImages1.value[groupIndex]) {
            groupedImages1.value[groupIndex] = [];
        }
        groupedImages1.value[groupIndex].push(image);
    });
};







const modules2 = import.meta.glob('../assets/img/ticbcs_gallery2/*.{png,jpg,jpeg,svg}', { eager: true, query: '?url', import: 'default' });

const galleryImages2 = ref<string[]>(Object.values(modules2) as string[]);

const groupedImages2 = ref<string[][]>([]);


const groupImages2 = () => {
    groupedImages2.value = []; // 清空之前的分組
    galleryImages2.value.forEach((image, index) => {
        const groupIndex = Math.floor(index / cols.value);
        if (!groupedImages2.value[groupIndex]) {
            groupedImages2.value[groupIndex] = [];
        }
        groupedImages2.value[groupIndex].push(image);
    });
};


onMounted(() => {
    window.addEventListener('resize', handleResize);
    handleResize(); // 初始調用以設置列數
});

onUnmounted(() => {
    window.removeEventListener('resize', handleResize);
});



</script>
<style lang="scss" scoped>
.common-section {
    margin: $common-section-margin;
    width: $common-section-width;
    font-family: $common-section-font-family;
    justify-content: center;
    align-items: center;
    display: flex;
    flex-direction: column;
    gap: 2.5rem;

    .title {
        font-size: 2rem;
        font-weight: 700;
        margin: 0rem 0 1rem 0;
    }

    .gallery {
        border-width: 0px 0 1px 0;
        border-style: solid;
        border-color: #D3D3D3;


        .image-group {
            display: flex;
            justify-content: flex-start;
            align-items: center;
            gap: 2rem;
            margin-bottom: 1rem;
            width: 100%;
            min-width: 100%;

            .image-item {
                width: calc(100% / 6 - 2rem);

                img {
                    width: 100%;
                    height: auto;
                    max-width: 100%;
                    max-height: 100%;
                    object-fit: cover;
                }

                
                
            }
            @media screen and (max-width: 768px) {
                // width: calc(100% / 2 - 2rem);
                justify-content: center ;
                .image-item {
                    // width: calc(100% / 2 );
                    flex: 1;
                }
            }

            @media screen and (max-width: 1024px) {
                // width: calc(100% / 3 - 2rem);
                justify-content: center;

                .image-item {
                    width: calc(100% / 3 - 2rem);
                }
            }
        }
    }

}
</style>