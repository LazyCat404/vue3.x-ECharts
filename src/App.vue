<template>
    <div id="app">
        <router-view/>
    </div>
</template>

<style>
    /* 这里的样式是公用的，作用于每个组件 */
    *{
        padding: 0;
        margin: 0;
    }
    html,body,#app{
        height: 100%;
        width: 100%;
        overflow: hidden;
    }
    body{
        background: url("../public/images/bg.jpg");
    }
</style>
