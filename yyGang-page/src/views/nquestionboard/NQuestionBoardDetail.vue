<template>
    <div>
        <DepartmentForm submit-button-text="수정" :init-form-data="initFormData"
            @form-submit="formSubmit"/>
    </div>
</template>

<script setup>
    import { useRoute, useRouter } from 'vue-router';
    import NQuestionBoardForm from '@/components/forms/NQuestionBoardForm.vue';
    import apiClient from '@/api';
    import { onMounted, reactive } from 'vue';

    const router = useRouter();
    const currentRoute = useRoute(); 
    const initFormData = reactive({});

    const fetchNQuestionBoard = async (no) => {
        try {
            const response = await apiClient.get(
                `/NutrientQuestion/{nSupplementId}/{nqboardId}/${no}`
            );

            Object.assign(initFormData, response.data.items[0]);
        } catch (error) {
            if (error.response.data.code === 404) {
                alert(error.response.data.message);

                router.push({name: 'departments'});
            } else {
                alert('에러가 발생했습니다.');
            }
        }
    };

    const formSubmit = async (formData) => {
        try {
            const response = await apiClient.put(
                `/NutrientQuestion/{nSupplementId}/{nqboardId}/${formData.no}`,
                formData
            );

            if(response.data.code === 200) {
                alert('정상적으로 수정되었습니다.');
            }
        } catch (error) {
            if (error.response.data.code === 400) {
                alert('학과 정보를 모두 입력해 주세요.');
            } else if (error.response.data.code === 404) {
                alert(error.response.data.message);

                router.push({name: 'NQuestionBoard'});
            } else {
                alert('에러가 발생했습니다.');
            }
        }
    };

    onMounted(() => {
        fetchNQuestionBoard(currentRoute.params.no);
    });
</script>

<style scoped>

</style>