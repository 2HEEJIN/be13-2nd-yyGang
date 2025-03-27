<template>
    <div class="container" style="background-color: #FDF9F0">
        <h3 class="ps-5">상품 문의 등록</h3>
        <hr style="border: 2px solid #289631">
        <br>
        <p class="ps-5">
            상품 문의는 상품의 배송, 반품/취소, 교환/변경 등의 구매 과정에 대해 상품의 판매자에게 문의하는 게시판입니다. 
            <br><br>
            문의사항은 휴일을 제외한 최대 2-3일이 소요될 수 있습니다.
            <br>
            더 빠른 해결을 원하시면 전화 상담 또는 카카오톡 플러스 친구 > 1:1 문의하기 메뉴로 가능합니다.
            <br><br>
            문의사항 작성 시 개인정보 유출에 주의해주세요. 작성자의 부주의로 인한 개인정보 유출 피해의 책임은 본인에게 있습니다.
            <br><br>
            비방, 욕설, 광고글 등 구매 관련 문의와 관련 없는 게시글은 삭제될 수 있습니다.
            <br><br>
        </p>
        <hr style="border: 2px solid #289631">
    </div>
    <div>
        <form @submit.prevent="submitClick">
            <div class="input-form border-bottom pb-5" >
                <div class="input-group mb-3 row">
                    <span class="input-title input-group-text col-2" id="basic-addon1"> 제목</span>
                    <input type="text" class="form-control col-10" placeholder="제목을 입력하세요" aria-label="Username" aria-describedby="basic-addon1" v-model="formData.title">
                </div>
                <div class="input-group row">
                    <span class="input-content input-group-text col-2 ">내용</span>
                    <textarea class="form-control col-10" aria-label="With textarea" placeholder="내용을 입력하세요" v-model="formData.content"></textarea>
                </div>
            </div>

            <div class="btn-section d-flex mt-5 mb-5">
                <button class="cancel-btn btn btn-outline-secondary fs-5" type="button" @click="buttonClick">취소하기</button>
                <button class="submit-btn btn btn-outline-secondary fs-5" type="submit">등록하기</button>
            </div>
        </form>
    </div>
</template>

<script setup>
    import { reactive, watch } from 'vue';
    import { useRouter } from 'vue-router';

    const router = useRouter();
    const formData = reactive({
        title: '',
        content: ''
    });

    const emit = defineEmits(['form-submit']);

    const props = defineProps({
        submitButtonText: String,
        questionboard: Object
    });

    const submitClick = () => {
    if (!formData.title.trim() || !formData.content.trim()) {
        alert('제목과 내용을 모두 입력해주세요.');
        return;
    }
    
    submitQuestion();
    
    emit('form-submit', formData);
    };

    const buttonClick = ()=>{
        router.back();    
    };

    watch(
        props.nquestionboard,
        (newFormData)=>{
            Object.assign(formData, newFormData);
        },
        {immediate: true}
    );

    const submitQuestion = () => {
    console.log("등록된 문의:", formData);
    
    alert('문의가 등록되었습니다.');
    
    router.push('/NQuestionBoard');
};
</script>

<style scoped>

.input-form{
    width: 90%;
    margin: 0 auto;
}

.input-title{
    min-height: 55px;
    justify-content: center;
}
.input-content{
    min-height: 300px;
    align-items: flex-start;
    justify-content: center;
}

.btn-section{
    width: 90%;
    margin: 0 auto;
    justify-content: space-evenly;
    
}

.submit-btn, .cancel-btn{
    width: 25%;
    border-radius: 20px 0px 20px 0px;
    border-color: #BDBDBD;
    box-shadow: 5px 5px 10px 0 lightgray;   
}

.submit-btn{
    background-color: #A0D683;
}
</style>