<template>
  <div>
    <br />
    <v-card>
      <v-card-title>{{header}}</v-card-title>
      <v-data-table :headers="headers" :items="asteroids" class="elevation-1">
        <template slot="headerCell" slot-scope="props">
          <v-tooltip bottom>
            <template v-slot:activator="{ on }">
              <span v-on="on">{{ props.header.text }}</span>
            </template>
            <span>{{ props.header.text }}</span>
          </v-tooltip>
        </template>
        <template v-slot:items="props">
          <td>{{ props }}</td>
          <!-- <td class="text-xs-right">{{ props.item.index }}</td>
          <td class="text-xs-right">{{ props.item.name }}</td>
          <td class="text-xs-right">{{ props.item.close_approach_data[0].close_approach_date}}</td>
          <td class="text-xs-right">{{ props.item.close_approach_data[0].miss_distance.miles }}</td>-->
          <!-- <td class="text-xs-right">{{ props.item.remove }}</td> -->
        </template>
      </v-data-table>
    </v-card>
  </div>
</template>

<script>
export default {
  props: ["asteroids", "header"],

  computed: {},
  methods: {},

  data() {
    return {
      headers: [
        {
          text: "#",
          align: "left",
          sortable: false,
          value: "index"
        },
        { text: "Name", value: "name" },
        {
          text: "Close Approach Date",
          value: "close_approach_data[0].close_approach_date"
        },
        {
          text: "Miss Distance (mi)",
          value: "close_approach_data[0].miss_distance.miles"
        }
      ]
    };
  }
};
</script>
<style>
</style>