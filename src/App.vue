<script setup>
import { ref, computed } from "vue"
    const products = ref([
{
    id: 1,
    name: 'iphone',
    date: '20.11.2024',
    count: 100,
    price: 1500,
},
{
    id: 1,
    name: 'Oppo',
    date: '25.11.2024',
    count: 177,
    price: 155,
},
{
    id: 1,
    name: 'redmi',
    date: '20.07.2024',
    count: 700,
    price: 100,
},
{
    id: 1,
    name: 'poco',
    date: '08.08.2024',
    count: 100000,
    price: 223,
},
    ]);
const name = ref('');
const date = ref('');
const count = ref(1);
const price = ref(0)

const addProduct = () => {
    if (name.value && date.value && count.value && price.value) {
products.value.push(
            {
                id: Date.now(),
                name: name.value,
                date: (new Date(date.value)). toLocaleDateString(),
                count: count.value,
                price: price.value,
            }
        )
    }
}

const removeProduct = (id) => {
    products.value = products.value.filter((product) => product.id != id) 
}

const totalSum = computed(() => {
    return products.value.reduce((sum, product) => sum + (product.price * product.count), 0)
})
</script>

<template>
<div class="container">
    <div class="row">
        <div class="col">
            <h1 class="text-center mt-4">Учёт товаров</h1>
            <form action="">
                <div class="mb-3">
                    <label for="date" class="form-label">Название</label>
                    <input type="text" v-model="name" class="form-control" :class="{'is-invalid': !name}" id="name" >
                    <div class="invalid-feedback">
                        Заполните пожалуйста название
                    </div>
                </div>
                <div class="mb-3">
                    <label for="date" class="form-label">Дата</label>
                    <input type="date" v-model="date" class="form-control" :class="{'is-invalid': !date}" id="name" >
                    <div class="invalid-feedback">
                        Заполните пожалуйста дату
                    </div>
                </div>
                <div class="mb-3">
                    <label for="date" class="form-label">Количество</label>
                    <input type="number" v-model="count" class="form-control" :class="{'is-invalid': !count}" id="name" >
                    <div class="invalid-feedback">
                        Заполните пожалуйста количество
                    </div>
                </div>
                <div class="mb-3">
                    <label for="date" class="form-label">Цена</label>
                    <input type="number" v-model="price" class="form-control" :class="{'is-invalid': !price}" id="name" >
                    <div class="invalid-feedback">
                        Заполните пожалуйста цену
                    </div>
                </div>
                <div class="text-center mb-3">
                    <button @click="addProduct" type="button" class="btn btn-dark">Добавить</button>
                </div>
            </form>
        </div>
    </div>
    <div class="row row-cols-1 row-cols-md-3 g-4">
  <div class="col" v-for="product in products" :key="product.id">
    <div class="card h-100">
        <div class="card-body">
            <h5 class="card-title">{{ product.name }}</h5>
            <p class="card-text">{{ product.date }}</p>
            <p class="card-text">${{ product.price }}</p>
            <p class="card-text">x{{ product.count }}</p>
        </div>
        <div class="cart-footer text-end">
            <button @click="removeProduct(product.id)" type="button" class="btn btn-secondary">Удалить</button>
        </div>
    </div>
  </div>
</div>
<div class="row my-4">
    <div class="col">
        <h3 class="text-end">Общая сумма: ${{totalSum}}</h3>
    </div>
</div>



</div>

</template>

