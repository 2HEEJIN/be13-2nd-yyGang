<template>
    <table class="table table-striped table-hover text-center">
        <thead>
            <tr>
                <th>No</th>
                <th>상태</th>
                <th>제목</th>
                <th>작성자</th>
                <th>등록일</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="nboardlist in NQuestionBoard" :key="nboardlist.no"
                @click.stop="emit('item-click', nboardlist.no);">
                <td>{{ nboardlist.idx }}</td>
                <td>{{ nboardlist.status }}</td>
                <td>{{ nboardlist.title }}</td>
                <td>{{ nboardlist.author }}</td>
                <td>{{ nboardlist.created_at }}</td>
                <td>
                    <button type="button" class="btn btn-outline-danger"
                        @click.stop="confirmDelete(NQuestionBoard.no);">삭제</button>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script setup>
    const props = defineProps({
        NQuestionBoard: {
            type: Array,
            required: true
        }
    });

    const emit = defineEmits(['item-click', 'delete-NQuestionBoard']);

    const confirmDelete = (no) =>{
        if(confirm('정말로 삭제하시겠습니까?')) {
            emit('delete-NQuestionBoard', no);
        }
    }
</script>

<style scoped>

</style>