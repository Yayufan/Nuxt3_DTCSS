<template>
    <div class="mobile-section">
        <div class="mobile-menu">
            <ol>
                <div v-for="item in menu">
                    <li @click="handleClick(item.path)" :class="activeClass(item.path)">
                        {{ item.title }}
                    </li>
                    <!-- <li @click="item.isActive = !item.isActive">
                        {{ item.title }}
                    </li> -->
                </div>
            </ol>
        </div>
        <div class="gray-section" @click="closeMenu"></div>

    </div>
</template>
<script lang="ts" setup>



const emits = defineEmits(['closeMenu']);

const closeMenu = () => {
    emits('closeMenu');
}

const menu = reactive([
    { title: '首頁', path: '/', isActive: false },
    { title: '關於我們', path: '/about-us', isActive: false },
    { title: '會議資訊', path: '/conference-information', isActive: false },
    { title: '註冊資訊', path: '/seminar-registration',isActive: false },
    { title: '交通資訊', path: '/transportation',isActive: false },
    { title: '旅遊資訊', path: '/travel',isActive: false },
    { title: '贊助廠商', path: '/sponsor-list',isActive: false },
    { title: '吉祥物專區', path: '/mascot',isActive: false },

])


const activeItem = ref('')
const setActiveItem = (item: any) => {
    item.isActive = !item.isActive
    activeItem.value = item.title
}

const activeClass = (item: string) => {
    return router.currentRoute.value.path === item ? 'active' : ''
}

const router = useRouter()
console.log('router', router.currentRoute.value.path);

const handleClick = (path: string) => {
    router.push(path)
    closeMenu()
}



const headToLogin = () => {
    closeMenu();
    let url = isLogin.value ? '/member-center' : '/login';
    router.push(url);
}

const isLogin = ref(false);
const validateLogin = () => {
    let res = localStorage.getItem('Authorization-member');
    if (res) {
        isLogin.value = true;
    }
}

router.beforeEach(async (to, from, next) => {
    validateLogin();
    next();
});

const logout = async () => {
    let res = await CSRrequest.post('/member/logout');
    if (res.code === 200) {
        localStorage.removeItem('Authorization-member');
        isLogin.value = false;
        router.push('/login');
    }
}


</script>
<style lang="scss" scoped>

.mobile-menu {
    background-color: black;
    height: 100vh;
    width: 60%;
    position: fixed;
    top: 0rem;
    left: 0rem;
    z-index: 10;
    transition: 0.5s;


    ol {
        list-style: none;
        padding: 2rem 2rem;

        li {
            padding: 1rem;
            font-size: 1.3rem;
            font-weight: bold;
            color: white;

            img {
                width: 1.5rem;
                margin-right: 0.5rem;
                position: relative;
                top: 3px;
            }

            .arrow {
                width: 1rem;
                margin-left: 1rem;
                transform: rotateZ(-90deg);
                position: relative;
                top: 1px;
            }

            .is-active {
                transform: rotateZ(0deg);
            }

            &:hover {
                cursor: pointer;
            }

            &.active {
                color: #FF5529;
                border-radius: 10px;
            }
        }

        .submenu {
            overflow: hidden;
            max-height: 0px;
            transition: 0.5s;
            font-size: 16px;

            a {
                font-size: 1.2rem;
                font-weight: bold;
                display: block;
                color: $main-content-color;
                padding: 0.5rem 0;
            }

            &.is-open {
                overflow: auto !important;
                max-height: none !important;
                margin-left: 15vw;
                font-size: 16px;
            }
        }
    }
}

.gray-section {
    background-color: #F0F0F0;
    opacity: 0.5;
    height: 100vh;
    width: 40%;
    position: fixed;
    top: 0rem;
    right: 0rem;
    z-index: 10;
}
</style>