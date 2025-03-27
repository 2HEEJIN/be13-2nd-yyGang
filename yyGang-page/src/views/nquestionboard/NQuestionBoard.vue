<template>
    <div class="table table-striped table-hover text-center">
        <div class="d-flex mb-3">
            <h5 style="text-align: left; " class="header" >Q&A    |    상품에 대해 궁금한 점 있으면 문의해주세요.</h5>
            <div class="common-buttons">
                <button type="button" class="custom-button me-3" @click="fnQuestionBoardWrite">문의 하기</button>
                <button type="button" class="custom-button" @click="fnMyQuestions">내 문의 글 확인</button>
            </div>
        </div>
        <table class="w3-table-all container border-bottom" >
        <thead class="theader"> 
            <tr>
                <th>No</th>
                <th>상태</th>
                <th>제목</th>
                <th>작성자</th>
                <th>등록일시</th>
            </tr>
        </thead>
        <tbody >
            <tr v-for="(row, idx) in nboardlist" :key="idx" class="content">
                <td>{{ row.idx }}</td>
                <td>{{ row.status }}</td>
                <td>{{ row.title }}</td>
                <td>{{ row.author }}</td>
                <td>{{ row.created_at }}</td>
            </tr>
        </tbody>
        </table>

        <div class="pagination w3-bar w3-padding-16 w3-small" v-if="pageInfo.totalCount > 0">
            <span class="pg">
                <a @click="fnPage(1)" class="first w3-button w3-border">&lt;&lt;</a>
                <a v-if="pageInfo.start_page > 10" @click="fnPage(pageInfo.start_page - 1)" class="prev w3-button w3-border">&lt;</a>
            <template v-for="n in paginavigation()" :key="n">
                <strong v-if="pageInfo.page === n" class="w3-button w3-border w3-green">{{ n }}</strong>
                <a v-else class="w3-button w3-border" @click="fnPage(n)">{{ n }}</a>
            </template>
                <a v-if="pageInfo.total_page_cnt > pageInfo.end_page" @click="fnPage(pageInfo.end_page + 1)" class="next w3-button w3-border">&gt;</a>
                <a @click="fnPage(pageInfo.total_page_cnt)" class="last w3-button w3-border">&gt;&gt;</a>
            </span>
        </div>
    </div>
</template>

<script setup>
    import { ref, onMounted } from 'vue';
    import { useRoute, useRouter } from 'vue-router';

    const route = useRoute();
    const router = useRouter();

    const nboardlist = ref([]);
    const pageInfo = ref({
        currentPage: 1,
        totalCount: 0,
        pageLimit: 5,
        listLimit: 10,
        total_page_cnt: 0,
        start_page: 1,
        end_page: 5,
    });

    // 고정 데이터로 가져올 예시 (서버에서 실제 데이터가 들어오면 수정 필요)
    const fnGetnboardlist = (page) => {
        try {
            const allData = [
                { idx: 1, status: '답변 완료', title: '배송이 언제 올까요?', author: 'cus*****@naver.com', created_at: '2024-03-25' },
                { idx: 2, status: '답변 완료', title: '상품이 파손됐는데요', author: 'cus*****@naver.com', created_at: '2024-03-24' },
                { idx: 3, status: '답변 대기', title: '집에 가고 싶은데 어쩌죠?', author: 'cus*****@naver.com', created_at: '2024-03-23' },
                { idx: 4, status: '답변 대기', title: '상품이 잘못 왔어요.', author: 'cus*****@naver.com', created_at: '2024-03-22' },
                { idx: 5, status: '답변 완료', title: '환불이 가능한가요?', author: 'cus*****@naver.com', created_at: '2024-03-21' },
        ];

    // 페이지네이션 적용
    const startIndex = (page - 1) * pageInfo.value.listLimit;
    const endIndex = startIndex + pageInfo.value.listLimit;
        nboardlist.value = allData.slice(startIndex, endIndex);

    // 페이지 정보 업데이트
        pageInfo.value.totalCount = allData.length;
        pageInfo.value.total_page_cnt = Math.ceil(allData.length / pageInfo.value.listLimit);
        pageInfo.value.start_page = Math.floor((page - 1) / pageInfo.value.pageLimit) * pageInfo.value.pageLimit + 1;
        pageInfo.value.end_page = Math.min(pageInfo.value.start_page + pageInfo.value.pageLimit - 1, pageInfo.value.total_page_cnt);
        } catch (error) {
            alert('데이터를 불러오는 중 오류가 발생했습니다.');
        }
    };

    // 페이지 변경 시 호출되는 함수
    const fnPage = (page) => {
        pageInfo.value.currentPage = page;
        fnGetnboardlist(page);
    };

    // 페이지네이션의 페이지 번호를 반환
    const paginavigation = () => {
        let pageNumber = [];
        for (let i = pageInfo.value.start_page; i <= pageInfo.value.end_page; i++) {
        pageNumber.push(i);
        }
            return pageNumber;
    };

    const fnQuestionBoardWrite = () => {
        router.push('/QuestionBoardWrite');
    };

    // 내 문의 글 확인 버튼 클릭 시 내 문의 목록 페이지로 이동
    const fnMyQuestions = () => {
        router.push('/MyQuestions');
    };

    // 페이지 로드 시 데이터 불러오기
    onMounted(() => {
        fnGetnboardlist(pageInfo.value.currentPage);
    });
</script>

<style scoped>
    .header{
        margin: auto 0;
    }

    .content{
        color: #A19C9C;
    }

    .common-buttons{
        margin-left: auto;

    }

    .theader{
        border-top: 2px solid;
        border-bottom: 2px solid;
        border-color: #289631;
    }
    .container {
        padding: 20px;
    }
    .custom-button {
        background-color: #E8F5E9;
        color: #2D3A1A;
        padding: 4px 5px;
        font-size: 13px;
        border: none;
        border-radius: 8px;
        /* margin-bottom: 30px; */
        cursor: pointer;
    }
    .pagination {
        display: flex;
        justify-content: center;
        margin-top: 20px;
        gap: 5px;
    }
</style>
