<template>
    <form @submit.prevent="submitClick">
        <div class="mb-3">
            <label for="idx" class="form-label">No</label>
            <input type="number" class="form-control" id="idx" v-model.trim="formData.idx">
        </div>
        <div class="mb-3">
            <label for="status" class="form-label">상태</label>
            <input type="text" class="form-control" id="status" v-model.trim="formData.status">
        </div>
        <div class="mb-3">
            <label for="title" class="form-label">제목</label>
            <input type="text" class="form-control" id="title" v-model.trim="formData.title">
        </div>
        <div class="mb-3">
            <label for="author" class="form-label">작성자</label>
            <input class="form-control" id="author" v-model="formData.author">
        </div>
        <div class="mb-3">
            <label for="date" class="form-label">등록일</label>
            <input type="date" class="form-control" id="date" v-model.number="formData.date">
        </div>
        <button type="submit" class="btn btn-primary" v-text="submitButtonText"></button>
    </form>
</template>

<script setup>

</script>

<style scoped>

</style>