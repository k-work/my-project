<template>
    <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" @select="handleSelect">
        <el-menu-item index="1"><i class="el-icon-document"></i>{{ avatar }}</el-menu-item>
        <el-menu-item index="2"><i class="el-icon-user"></i>{{ login }}</el-menu-item>
        <el-submenu index="3">
            <template slot="title">{{ text }}</template>
            <el-menu-item index="2-1">EN</el-menu-item>
            <el-menu-item index="2-2">zh-CN</el-menu-item>
            <el-menu-item index="2-3">zh-TW</el-menu-item>
            <el-menu-item index="2-4">JP</el-menu-item>
        </el-submenu>
    </el-menu>
</template>

<style scoped lang="scss">
::v-deep.el-menu-demo {
    display: flex;
    justify-content: flex-end;
}
::v-deep.el-menu.el-menu--horizontal {
    border: none;
}
::v-deep.el-menu--horizontal>.el-menu-item.is-active {
    border: none;
}
</style>

<script>

export default {
    name: 'NavBar',
    props: {
        avatar: String,
        login: String,
        text: String,
    },
    data() {
        return {
            activeIndex: '1',
            activeIndex2: '1'
        };
    },
    methods: {
        handleSelect(key, keyPath) {
            console.log(key, keyPath);
        }
    }
}

</script>