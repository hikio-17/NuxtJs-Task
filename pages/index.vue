<template>
  <div class="">
    <header>
      <Header />
    </header>
    <main>
      <div class="container-fluid">
        <div class="title border-bottom d-flex align-items-center py-2 mt-4">
          <h4>Task</h4>
          <div class="d-flex align-items-center ms-auto">

            <!-- SEARCH -->
            <input type="text" class="form-control" placeholder="Search" v-model="searchQuery">

            <!-- DROPDOWN -->
            <select class="form-select ms-3" aria-label="Default select example" @change="setCategory($event)"
              v-model="searchCategory">
              <option selected value="" disabled>Search by category</option>
              <option selected value="" >All</option>
              <option value="Category 1">Category 1</option>
              <option value="Category 2">Category 2</option>
              <option value="Category 3">Category 3</option>
            </select>

            <!-- OPTION VIEWS -->
            <div class="d-flex align-items-center justify-content-end w-100 ms-3">
              <span class="me-2">View As</span>
              <button class="btn btn-outline-secondary py-1 px-3" @click="isGrid = !isGrid">
                {{ isGrid ? 'Grid' : 'List' }}
              </button>
            </div>
          </div>
        </div>

        <!-- Card List Item -->
        <div class="list-task row">
          <CardItem v-for="(task, i) in resultTask" :key="i" :task="task" :isGrid="isGrid" />
        </div>

        <!-- Form -->
        <div class="action py-2">
          <a href="#" class="add-button" v-if="!isCreating" @click="isCreating = !isCreating">Add Task</a>
          <div class="add-card" v-else>
            <div class="card mb-2">
              <div class="card-body d-flex flex-column p-0">
                <input type="text" class="form-control border-0 mb-2" placeholder="Title">
                <textarea class="form-control border-0 small" placeholder="Description"></textarea>
              </div>
            </div>
            <div class="button-wrapper d-flex">
              <button class="btn btn-primary me-2">Save</button>
              <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">Cancel</button>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import CardItem from '@/components/Card/CardItem.vue'
export default {
  name: 'IndexPage',
  components: {
    CardItem,
  },
  data() {
    return {
      tasks: [
        {
          title: 'Belajar Python',
          description: 'ini deskripsi',
          category: 'Category 1',
          isDone: false,
        },
        {
          title: 'Task 1',
          description: 'ini deskripsi',
          category: 'Category 2',
          isDone: false,
        },
        {
          title: 'Task 1',
          description: 'ini deskripsi',
          category: 'Category 3',
          isDone: false,
        },
        {
          title: 'belajar',
          description: 'ini deskripsi',
          category: 'Category 4',
          isDone: false,
        },
      ],
      isCreating: false,
      isGrid: false,
      searchQuery: '',
      searchCategory: ''
    };
  },
  methods: {
    setCategory(e) {
      this.searchCategory = e.target.value;
    }
  },
  computed: {
    resultTask() {
      if (this.searchQuery) {
        this.searchCategory = '';
        return this.tasks.filter((item) => {
          return this.searchQuery
          .toLowerCase()
          .split(' ')
          .every((v) => item.title.toLowerCase().includes(v));
        })
      }
      
      if (this.searchCategory) {
        return this.tasks.filter((item) => item.category.toLowerCase() === this.searchCategory.toLowerCase());
      }

      return this.tasks;
    }
  },
};
</script>
