<script setup>
import { onMounted } from "vue";
import { initFlowbite } from "flowbite";

const { pending, data: posts } = useFetch("https://fakestoreapi.com/products", {
  lazy: true,
});

const categories = ref("");
const filteredCategory = ref([]);
filteredCategory.value = posts.value;

console.log("lagi debug : ", filteredCategory.value);

function lessDescription(description) {
  return description.substring(0, 100);
}

function lessTitle(title) {
  return title.substring(0, 30);
}

function filterCategory() {
  filteredCategory.value = posts.value.filter((post) => {
    return post.category === categories.value;
  });
}

function callCategory(category) {
  categories.value = category;
  filterCategory();
}

function callAllCategory() {
  filteredCategory.value = posts.value;
}

// function filterByRangePrice(min, max) {
//   filteredCategory.value = posts.value.filter((post) => {
//     return post.price >= min && post.price <= max;
//   });
// }

onMounted(() => {
  initFlowbite();
  filteredCategory.value = posts.value;
});


</script>
<template>
  <NuxtLayout />

  <NuxtLayout name="default" />
  <div class="p-4 sm:ml-64">
    <div
      class="p-4 border-2 border-gray-200 border-dashed rounded-lg dark:border-gray-700"
    >
      <div class="flex items-end justify-center py-4 md:py-8 flex-wrap">
        <h2 class="text-base font-bold px-5 py-2.5 text-center mr-3 mb-3">
          Filter
        </h2>
        <button
          @click="callAllCategory('')"
          type="button"
          class="text-blue-700 hover:text-white border border-blue-600 bg-white hover:bg-blue-700 focus:ring-4 focus:outline-none focus:ring-blue-300 rounded-full text-base font-medium px-5 py-2.5 text-center mr-3 mb-3 dark:border-blue-500 dark:text-blue-500 dark:hover:text-white dark:hover:bg-blue-500 dark:bg-gray-900 dark:focus:ring-blue-800"
        >
          All categories
        </button>
        <button
          @click="callCategory('women\'s clothing')"
          type="button"
          class="text-gray-900 border border-white hover:border-gray-200 dark:border-gray-900 dark:bg-gray-900 dark:hover:border-gray-700 bg-white focus:ring-4 focus:outline-none focus:ring-gray-300 rounded-full text-base font-medium px-5 py-2.5 text-center mr-3 mb-3 dark:text-white dark:focus:ring-gray-800"
        >
          Women's clothing
        </button>
        <button
          @click="callCategory('jewelery')"
          type="button"
          class="text-gray-900 border border-white hover:border-gray-200 dark:border-gray-900 dark:bg-gray-900 dark:hover:border-gray-700 bg-white focus:ring-4 focus:outline-none focus:ring-gray-300 rounded-full text-base font-medium px-5 py-2.5 text-center mr-3 mb-3 dark:text-white dark:focus:ring-gray-800"
        >
          Jewelery
        </button>

        <button
          @click="callCategory('electronics')"
          type="button"
          class="text-gray-900 border border-white hover:border-gray-200 dark:border-gray-900 dark:bg-gray-900 dark:hover:border-gray-700 bg-white focus:ring-4 focus:outline-none focus:ring-gray-300 rounded-full text-base font-medium px-5 py-2.5 text-center mr-3 mb-3 dark:text-white dark:focus:ring-gray-800"
        >
          Electronics
        </button>

        <button
          @click="callCategory('men\'s clothing')"
          type="button"
          class="text-gray-900 border border-white hover:border-gray-200 dark:border-gray-900 dark:bg-gray-900 dark:hover:border-gray-700 bg-white focus:ring-4 focus:outline-none focus:ring-gray-300 rounded-full text-base font-medium px-5 py-2.5 text-center mr-3 mb-3 dark:text-white dark:focus:ring-gray-800"
        >
          Men's clothing
        </button>

        <!-- <div class="px-1 py-1 text-center mr-3 mb-3">
          <input
            type="number"
            min="0"
            id="helper-text"
            aria-describedby="helper-text-explanation"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="min price"
          />
        </div>
        <div class="px-1 py-1 text-center mr-3 mb-3">
          <input
            type="number"
            min="0"
            id="helper-text"
            aria-describedby="helper-text-explanation"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="max price"
          />
        </div> -->
      </div>
      <div>
        <div v-if="pending">Loading ...</div>
        <div v-else class="grid grid-cols-2 md:grid-cols-3 gap-4">
          <div v-for="post in filteredCategory" class="p-1">
            <NuxtLink
              :to="`/products/${post.id}`"
              class="flex flex-row p-2 items-center bg-white border border-gray-200 rounded-lg shadow md:flex-row md:max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700"
            >
              <img
                class="max-w-[150px] max-h-[150px] rounded-t-lg h-96 md:h-auto md:w-48 md:rounded-[15px] md:rounded-l-lg"
                :src="post.image"
                :alt="post.title"
              />
              <div class="flex flex-col justify-between p-4 leading-normal">
                <h5
                  class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white overflow-y-hidden ..."
                >
                  {{ lessTitle(post.title) }}
                </h5>
                <p
                  class="mb-3 text-ellipsis overflow-hidden font-normal text-gray-700 dark:text-gray-400"
                >
                  {{ lessDescription(post.description) }}
                </p>
              </div>
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
