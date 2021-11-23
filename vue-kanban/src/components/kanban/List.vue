<template>
<div class="lists_box">
    <div class='stit'>{{ title }}</div>
    <ul class='work_list'>
        <li :key="i" v-for="(li, i) in list" @click="goView(li.idx)">{{ li.subject }}</li>
    </ul>
</div>
</template>
<script>
import kanban from "../../models/kanban.js"
export default {
    mixins: [kanban],
    data() {
        return {
            title : "",
            list : [],
        };
    },
    props : {
        status : {
            type : String,
            default : "ready",
        }
    },
    async mounted() {
        switch(this.status) {
            default : 
                this.title = "To Do"; //사용자가 입력해서 받아오는거 -> 카테고리 같은..?(ex.shopping, study...)
                break;
            case "progress": 
                this.title = "Working";
                break;
            case "done" : 
                this.title = "Done";
        }

        this.list = await this.$getList(this.status);
    },
    methods : {
        goView(idx) {
            this.$router.push({ path : "/kanban/view", query : { idx }});
        }
    }
}
</script>