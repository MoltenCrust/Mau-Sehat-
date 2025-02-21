<template>
    <div class="main-container">
        <div class="table">
            <DataTable :value="products" 
                      :scrollable="true" 
                      scrollHeight="calc(100vh - 4rem)"
                      tableStyle="width: 100%"
                      paginator :rows="10" :rowsPerPageOptions="[5, 10, 20, 50]">
                <Column field="code" header="Speaker ID"></Column>
                <Column field="name" header="Painting Title"></Column>
                <Column field="category" header="Speaker Status"></Column>
                <Column field="quantity" header="Current Language"></Column>
            </DataTable>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { ProductService } from '@/service/ProductService';

onMounted(() => {
    ProductService.getProducts().then((data) => (products.value = data));
});

const products = ref();
</script>

<style scoped>
.main-container {
    height: 100%;
    width: 95%;
    box-sizing: border-box;
    margin-top: 1rem;
}

.table {
    height: 100%;
    width: 100%;
}

/* Optional: Make columns take up equal space */
:deep(.p-datatable) {
    border-radius: 10pt 10pt 10pt 10pt !important;
    overflow: hidden; /* This ensures inner elements don't overflow the rounded corners */
}

/* Remove border radius from paginator */
:deep(.p-paginator) {
    border-radius: 0pt 0pt 10pt 10pt !important;
}
</style>