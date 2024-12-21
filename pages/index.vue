<script setup>
const items = [
  {
    title: 'Item #1',
    value: 1,
  },
  {
    title: 'Item #2',
    value: 2,
  },
  {
    title: 'Item #3',
    value: 3,
  },
];

const content = ref("");

function onList(text) {
  content.value = `${text} がクリックされました。`;
}

function onListMenu(text) {
  content.value = `${text} のメニューがクリックされました。`;
}
</script>
<template>
  <div>
    <!-- list -->
    <v-card
      class="ma-5"
      max-width="600"
    >
      <v-list>
        <v-list-item
          v-for="item in items"
          :key="item.id"
          :title="item.title"
          @click="onList(item.title)"
        >
          <template v-slot:append>
            <v-menu>
              <template v-slot:activator="{ props }">
                <v-btn
                  color="grey"
                  icon="mdi-dots-horizontal"
                  variant="text"
                  v-bind="props"
                />
              </template>
              <v-list>
                <v-list-item
                  title="メニュー"              
                  @click.stop="onListMenu(item.title)"
                />
              </v-list>
            </v-menu>
          </template>
        </v-list-item>
      </v-list>
    </v-card>
    <!-- content -->
    <v-card
      class="ma-5"
      max-width="600"
    >
      <v-card-text>
        <div class="mb">
          {{ content }}
        </div>
      </v-card-text>
    </v-card>
    <!-- reset button -->
    <div
      class="ma-5"
    >
      <v-btn
        @click="content = ''"
      >
        リセット
      </v-btn>
    </div>
  </div>
</template>
