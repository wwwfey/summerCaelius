<template>
  <div class="row bg-cyan-2">
    <q-table
      flat bordered
      :rows="rows"
      :columns="columns"
      row-key="id"
      :filter="filter"
      :loading="loading"
      style="width: 100%; max-width: 100vw"
      :pagination="pagination"
      class="text-center bg-cyan-2"
    >

      <template v-slot:top>
        <h6>My Favorite Food is healthy?</h6>
        <q-space/>
        <q-input dense debounce="300" color="primary" v-model="filter">
          <template v-slot:append>
            <q-icon name="search"/>
          </template>
        </q-input>
      </template>

    </q-table>
  </div>

</template>

<script>
import {ref} from 'vue'

const columns = [
  {
    name: 'name',
    required: true,
    label: 'Dessert (100g serving)',
    align: 'left',
    field: row => row.name,
    format: val => `${val}`,
    sortable: true
  },
  {name: 'calories', align: 'center', label: 'Calories', field: 'calories', sortable: true},
  {name: 'fat', label: 'Fat (g)', field: 'fat', sortable: true},
  {name: 'carbs', label: 'Carbs (g)', field: 'carbs'},
  {name: 'protein', label: 'Protein (g)', field: 'protein'},
  {name: 'sodium', label: 'Sodium (mg)', field: 'sodium'},
  {
    name: 'calcium',
    label: 'Calcium (%)',
    field: 'calcium',
    sortable: true,
    sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
  },
  {name: 'iron', label: 'Iron (%)', field: 'iron', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)}
]

const originalRows = [
  {
    name: 'Pizza (Margherita)',
    calories: 285,
    fat: 10.6,
    carbs: 36.6,
    protein: 10.1,
    sodium: 590,
    calcium: '18%',
    iron: '13%'
  },
  {
    name: 'Sushi (Tuna roll)',
    calories: 184,
    fat: 2.1,
    carbs: 38.2,
    protein: 4.7,
    sodium: 24,
    calcium: '2%',
    iron: '5%'
  },
  {
    name: 'Chocolate cake',
    calories: 352,
    fat: 16.5,
    carbs: 49.9,
    protein: 3.9,
    sodium: 166,
    calcium: '1%',
    iron: '6%'
  },
  {
    name: 'Grilled steak (Ribeye)',
    calories: 318,
    fat: 24.8,
    carbs: 0,
    protein: 23.5,
    sodium: 55,
    calcium: '1%',
    iron: '11%'
  },
  {
    name: 'Lobster bisque',
    calories: 426,
    fat: 35.2,
    carbs: 11.6,
    protein: 16.4,
    sodium: 800,
    calcium: '12%',
    iron: '5%'
  },
  {
    name: 'Chicken curry',
    calories: 355,
    fat: 20.1,
    carbs: 15.7,
    protein: 26.8,
    sodium: 860,
    calcium: '6%',
    iron: '15%'
  },
  {
    name: 'Tacos (Al pastor)',
    calories: 150,
    fat: 7,
    carbs: 14,
    protein: 9,
    sodium: 250,
    calcium: '2%',
    iron: '6%'
  },
  {
    name: 'Risotto (Mushroom)',
    calories: 257,
    fat: 8.3,
    carbs: 38.2,
    protein: 7.2,
    sodium: 410,
    calcium: '5%',
    iron: '11%'
  },
  {
    name: 'Pho (Beef noodle soup)',
    calories: 367,
    fat: 11.1,
    carbs: 44.2,
    protein: 23.2,
    sodium: 1380,
    calcium: '11%',
    iron: '19%'
  },
  {
    name: 'Croissant',
    calories: 406,
    fat: 22,
    carbs: 44,
    protein: 8,
    sodium: 446,
    calcium: '2%',
    iron: '16%'
  },
  {
    name: 'Pad Thai',
    calories: 830,
    fat: 37,
    carbs: 99,
    protein: 25,
    sodium: 1080,
    calcium: '8%',
    iron: '20%'
  },
  {
    name: 'Crème brûlée',
    calories: 340,
    fat: 20,
    carbs: 35,
    protein: 5,
    sodium: 55,
    calcium: '10%',
    iron: '2%'
  },
  {
    name: 'Goulash',
    calories: 420,
    fat: 18,
    carbs: 11,
    protein: 54,
    sodium: 1240,
    calcium: '6%',
    iron: '35%'
  },
  {
    name: 'Chicken tikka masala',
    calories: 370,
    fat: 20,
    carbs: 15,
    protein: 30,
    sodium: 840,
    calcium: '10%',
    iron: '15%'
  },
  {
    name: 'Beef burger (with cheese and bacon)',
    calories: 780,
    fat: 47,
    carbs: 45,
    protein: 47,
    sodium: 1470,
    calcium: '20%',
    iron: '30%'
  },
  {
    name: 'Peking duck',
    calories: 484,
    fat: 33,
    carbs: 0,
    protein: 42,
    sodium: 400,
    calcium: '6%',
    iron: '20%'
  },
  {
    name: 'Ramen (Tonkotsu)',
    calories: 500,
    fat: 22,
    carbs: 59,
    protein: 15,
    sodium: 1870,
    calcium: '6%',
    iron: '20%'
  },
  {
    name: 'Paella',
    calories: 500,
    fat: 15,
    carbs: 70,
    protein: 20,
    sodium: 1000,
    calcium: '6%',
    iron: '20%'
  },
  {
    name: 'Tiramisu',
    calories: 452,
    fat: 26,
    carbs: 45,
    protein: 7,
    sodium: 60,
    calcium: '10%',
    iron: '8%'
  },
  {
    name: 'Fish and chips',
    calories: 840,
    fat: 43,
    carbs: 92,
    protein: 24,
    sodium: 1220,
    calcium: '6%',
    iron: '20%'
  },
  {
    name: 'Fajitas (Chicken)',
    calories: 380,
    fat: 19,
    carbs: 25,
    protein: 28,
    sodium: 950,
    calcium: '8%',
    iron: '15%'
  },
  {
    name: 'Lasagna',
    calories: 350,
    fat: 17,
    carbs: 32,
    protein: 19,
    sodium: 520,
    calcium: '15%',
    iron: '15%'
  },
  {
    name: 'Lobster roll',
    calories: 290,
    fat: 13,
    carbs: 28,
    protein: 17,
    sodium: 960,
    calcium: '6%',
    iron: '15%'
  },
  {
    name: 'Butter chicken',
    calories: 500,
    fat: 32,
    carbs: 10,
    protein: 45,
    sodium: 800,
    calcium: '10%',
    iron: '15%'
  },
  {
    name: 'Baklava',
    calories: 345,
    fat: 23,
    carbs: 33,
    protein: 6,
    sodium: 85,
    calcium: '4%',
    iron: '10%'
  },
  {
    name: 'BBQ ribs',
    calories: 455,
    fat: 30,
    carbs: 20,
    protein: 25,
    sodium: 1020,
    calcium: '4%',
    iron: '20%'
  },
  {
    name: 'Nachos (with melted cheese and guacamole)',
    calories: 540,
    fat: 34,
    carbs: 45,
    protein: 12,
    sodium: 830,
    calcium: '15%',
    iron: '15%'
  },
  {
    name: 'Poutine',
    calories: 590,
    fat: 38,
    carbs: 57,
    protein: 12,
    sodium: 890,
    calcium: '20%',
    iron: '25%'
  },
  {
    name: 'Miso soup',
    calories: 80,
    fat: 4,
    carbs: 7,
    protein: 5,
    sodium: 730,
    calcium: '2%',
    iron: '4%'
  },
  {
    name: 'Ceviche',
    calories: 150,
    fat: 5,
    carbs: 9,
    protein: 18,
    sodium: 470,
    calcium: '2%',
    iron: '15%'
  },
  {
    name: 'Cannoli',
    calories: 340,
    fat: 14,
    carbs: 48,
    protein: 6,
    sodium: 60,
    calcium: '10%',
    iron: '6%'
  },
  {
    name: 'Beef Wellington',
    calories: 650,
    fat: 45,
    carbs: 30,
    protein: 32,
    sodium: 680,
    calcium: '4%',
    iron: '20%'
  },
  {
    name: 'Chicken and waffles',
    calories: 790,
    fat: 42,
    carbs: 72,
    protein: 29,
    sodium: 1160,
    calcium: '20%',
    iron: '25%'
  },
  {
    name: 'Shrimp scampi',
    calories: 380,
    fat: 21,
    carbs: 23,
    protein: 25,
    sodium: 1060,
    calcium: '8%',
    iron: '15%'
  },
  {
    name: 'Biryani (Chicken)',
    calories: 460,
    fat: 16,
    carbs: 58,
    protein: 19,
    sodium: 950,
    calcium: '8%',
    iron: '20%'
  },
  {
    name: 'Chocolate mousse',
    calories: 410,
    fat: 30,
    carbs: 32,
    protein: 6,
    sodium: 30,
    calcium: '10%',
    iron: '8%'
  },
  {
    name: 'Beef pho (Vietnamese noodle soup)',
    calories: 450,
    fat: 15,
    carbs: 60,
    protein: 24,
    sodium: 1200,
    calcium: '4%',
    iron: '20%'
  },
  {
    name: 'Lobster thermidor',
    calories: 650,
    fat: 48,
    carbs: 12,
    protein: 35,
    sodium: 1020,
    calcium: '10%',
    iron: '25%'
  },
  {
    name: 'Tacos (Carnitas)',
    calories: 220,
    fat: 12,
    carbs: 18,
    protein: 13,
    sodium: 310,
    calcium: '4%',
    iron: '8%'
  },
  {
    name: 'Moussaka',
    calories: 380,
    fat: 23,
    carbs: 20,
    protein: 24,
    sodium: 600,
    calcium: '15%',
    iron: '15%'
  },
  {
    name: 'Chicken Parmesan',
    calories: 460,
    fat: 23,
    carbs: 29,
    protein: 35,
    sodium: 980,
    calcium: '20%',
    iron: '15%'
  },
  {
    name: 'Churros (with chocolate sauce)',
    calories: 290,
    fat: 15,
    carbs: 35,
    protein: 3,
    sodium: 40,
    calcium: '2%',
    iron: '10%'
  },
  {
    name: 'Gyoza (Japanese dumplings)',
    calories: 220,
    fat: 8,
    carbs: 26,
    protein: 10,
    sodium: 480,
    calcium: '2%',
    iron: '10%'
  },
  {
    name: 'Macarons',
    calories: 100,
    fat: 6,
    carbs: 11,
    protein: 2,
    sodium: 10,
    calcium: '0%',
    iron: '2%'
  },
  {
    name: 'Chicken Shawarma',
    calories: 470,
    fat: 22,
    carbs: 39,
    protein: 29,
    sodium: 1160,
    calcium: '6%',
    iron: '15%'
  },
  {
    name: 'Key lime pie',
    calories: 350,
    fat: 18,
    carbs: 43,
    protein: 5,
    sodium: 220,
    calcium: '10%',
    iron: '4%'
  },
  {
    name: 'Beef stroganoff',
    calories: 480,
    fat: 32,
    carbs: 10,
    protein: 38,
    sodium: 680,
    calcium: '6%',
    iron: '25%'
  },
  {
    name: 'Huevos rancheros',
    calories: 420,
    fat: 26,
    carbs: 29,
    protein: 20,
    sodium: 770,
    calcium: '10%',
    iron: '20%'
  },
  {
    name: 'Cheesecake (New York style)',
    calories: 420,
    fat: 32,
    carbs: 30,
    protein: 6,
    sodium: 300,
    calcium: '8%',
    iron: '6%'
  },
  {
    name: 'Chicken adobo',
    calories: 380,
    fat: 24,
    carbs: 10,
    protein: 30,
    sodium: 770,
    calcium: '4%',
    iron: '15%'
  }
];

export default {
  setup() {
    const loading = ref(false)
    const filter = ref('')
    const rowCount = ref(10)
    const rows = ref([...originalRows])
    const pagination = {
      page: 1,
      rowsPerPage: 10,
      total: 50
    }

    return {
      columns,
      rows,
      pagination,

      loading,
      filter,
      rowCount,

      // emulate fetching data from server
      addRow() {
        loading.value = true
        setTimeout(() => {
          const
            index = Math.floor(Math.random() * (rows.value.length + 1)),
            row = originalRows[Math.floor(Math.random() * originalRows.length)]

          if (rows.value.length === 0) {
            rowCount.value = 0
          }

          row.id = ++rowCount.value
          const newRow = {...row} // extend({}, row, { name: `${row.name} (${row.__count})` })
          rows.value = [...rows.value.slice(0, index), newRow, ...rows.value.slice(index)]
          loading.value = false
        }, 500)
      },

      removeRow() {
        loading.value = true
        setTimeout(() => {
          const index = Math.floor(Math.random() * rows.value.length)
          rows.value = [...rows.value.slice(0, index), ...rows.value.slice(index + 1)]
          loading.value = false
        }, 500)
      }
    }
  }
}
</script>
