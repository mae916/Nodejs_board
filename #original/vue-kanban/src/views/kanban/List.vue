<template>
<PageTitle>작업 목록</PageTitle>
<router-link to="/kanban/add" class='add_work'>작업추가</router-link>
<div class="lists-flex">
<List status="ready" />
<List status="progress" />
<List status="done" />
</div>
</template>
<script>
import PageTitle from "../../components/PageTitle.vue"
import List from "../../components/kanban/List.vue"
export default {
    components : {PageTitle, List},
    created() {
        if (!this.$isLogin() && this.$getToken()) {
            location.reload();
        }
    },
}
</script>