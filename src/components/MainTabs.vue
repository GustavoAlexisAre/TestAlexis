<template>
  <v-card>
    <v-toolbar color="primary">
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>Tablero principal</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>

      <template v-slot:extension>
        <v-tabs
          v-model="tab"
          align-tabs="title"
        >
          <v-tab
            v-for="item in itemsTab"
            :key="item"
            :value="item"
          >
            {{ item }}
          </v-tab>
        </v-tabs>
      </template>
    </v-toolbar>

    <v-window v-model="tab">
      <v-window-item
        v-for="item in itemsTab"
        :key="item"
        :value="item"
      >
        <v-card flat>

            <v-data-table
              :custom-filter="filterOnlyCapsText"
              :headers="headers"
              :items="items"
              :search="search"
              item-value="name"
            >
            
              <template v-slot:top>
                <v-text-field
                  v-model="search"
                  class="pa-2"
                  label="Search"
                ></v-text-field>
              </template>
              <template v-slot:item.actions="{ item }">
                <div class="text-center pa-4">
    <v-btn v-if="tab === 'Consulta' " @click="openModal(item)">
      Open Dialog
    </v-btn>

    <v-dialog
      v-model="dialog"
      width="auto"
    >
    <v-card max-width="400" prepend-icon="mdi-update">
        <v-card-title>{{ selectedItem.name }}</v-card-title>
        <v-card-text>
          <div>Cores: {{ selectedItem.cores }}</div>
          <div>Threads: {{ selectedItem.threads }}</div>
          <div>Base Clock: {{ selectedItem.baseClock }}</div>
          <div>Boost Clock: {{ selectedItem.boostClock }}</div>
          <div>Tdp: {{ selectedItem.tdp }}</div>
        </v-card-text>
        <template v-slot:actions>
          <v-btn
            class="ms-auto"
            text="Ok"
            @click="closeModal(item)"
          ></v-btn>
          
        </template>
      </v-card>
    </v-dialog>
  </div>
              </template>
            </v-data-table>

        </v-card>
      </v-window-item>
    </v-window>
  </v-card>


</template>

<script>
  export default {
    data () {
      return {
        tab: null,
        itemsTab: [
          'Consulta', 'Edición',
        ],
        text: '',
        search: '',
      headers: [
        {
          title: 'CPU Model',
          align: 'start',
          key: 'name',
        },
        {
          title: 'Cores',
          align: 'end',
          key: 'cores',
        },
        {
          title: 'Threads',
          align: 'end',
          key: 'threads',
        },
        {
          title: 'Base Clock',
          align: 'end',
          key: 'baseClock',
        },
        {
          title: 'Boost Clock',
          align: 'end',
          key: 'boostClock',
        },
        {
          title: 'TDP (W)',
          align: 'end',
          key: 'tdp',
        },
        { text: 'Acciones', value: 'actions', sortable: false },
      ],
      items: [
        {
          name: 'Intel Core i9-11900K',
          cores: 8,
          threads: 16,
          baseClock: '3.5 GHz',
          boostClock: '5.3 GHz',
          tdp: '125W',
        },
        {
          name: 'AMD Ryzen 9 5950X',
          cores: 16,
          threads: 32,
          baseClock: '3.4 GHz',
          boostClock: '4.9 GHz',
          tdp: '105W',
        },
        {
          name: 'Intel Core i7-10700K',
          cores: 8,
          threads: 16,
          baseClock: '3.8 GHz',
          boostClock: '5.1 GHz',
          tdp: '125W',
        },
        {
          name: 'AMD Ryzen 5 5600X',
          cores: 6,
          threads: 12,
          baseClock: '3.7 GHz',
          boostClock: '4.6 GHz',
          tdp: '65W',
        },
        {
          name: 'Intel Core i5-10600K',
          cores: 6,
          threads: 12,
          baseClock: '4.1 GHz',
          boostClock: '4.8 GHz',
          tdp: '125W',
        },
        {
          name: 'AMD Ryzen 7 5800X',
          cores: 8,
          threads: 16,
          baseClock: '3.8 GHz',
          boostClock: '4.7 GHz',
          tdp: '105W',
        },
        {
          name: 'Intel Core i3-10100',
          cores: 4,
          threads: 8,
          baseClock: '3.6 GHz',
          boostClock: '4.3 GHz',
          tdp: '65W',
        },
        {
          name: 'AMD Ryzen 3 3300X',
          cores: 4,
          threads: 8,
          baseClock: '3.8 GHz',
          boostClock: '4.3 GHz',
          tdp: '65W',
        },
        {
          name: 'Intel Pentium Gold G6400',
          cores: 2,
          threads: 4,
          baseClock: '4.0 GHz',
          tdp: '58W',
        },
        {
          name: 'AMD Athlon 3000G',
          cores: 2,
          threads: 4,
          baseClock: '3.5 GHz',
          tdp: '35W',
        },
      ],
      dialog: false,
      selectedItem: null,


      }
    },
    methods:{
      openModal(item) {
      console.log('Mostrar modal para:', item);
      this.selectedItem = item;
        this.dialog = true
    },
    closeModal(item){
      this.dialog = false
    }
    }

  }

</script>
