<template>
    <div class="container">
        <h3 class="border-bottom  pb-3">나의 문의</h3>
        <br>
        <table class="w3-table-all container border-bottom">
            <thead class="theader">
                <tr>
                    <th>번호</th>
                    <th>제목</th>
                    <th>상태</th>
                    <th>작성일</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="question in myquestions" :key="question.idx">
                    <td>{{ question.idx }}</td>
                    <td>
                        <router-link :to="{ name: 'myquestions' }">
                            {{ question.title }}
                        </router-link>
                    </td>
                    <td>{{ question.status }}</td>
                    <td>{{ question.created_at }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
    import { ref } from 'vue';

    // 예제 데이터 (실제 데이터는 API에서 받아올 수 있음)
    const myquestions = ref([
        { idx: 1, status: '답변 완료', title: '배송 문의' , created_at: '2024-03-25' },
        { idx: 2, status: '답변 완료', title: '환불 요청', created_at: '2024-03-24' },
        { idx: 3, status: '답변 대기', title: '상품 불량 문의', created_at: '2024-03-23' }
    ]);
</script>

<style scoped>
    .theader{
        border-top: 2px solid;
        border-bottom: 2px solid;
        border-color: #289631;
    }
    .container {
        padding: 20px;
    }
</style>