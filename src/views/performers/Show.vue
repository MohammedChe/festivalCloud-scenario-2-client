<template>
<b-col>
  <h2>Performer details</h2>
  <table id="table-performer" class="table table-hover">
    <tbody>
      <tr>
        <td><img :src="performer.image_path" height="200px" /></td>
      </tr>
      <tr>
        <td width="20%">Title</td>
        <td>{{ performer.title }}</td>
      </tr>
      <tr>
        <td>Description</td>
        <td>{{ performer.description }}</td>
      </tr>
      <tr>
        <td>Contact Email</td>
        <td>{{ performer.contact_email }}</td>
      </tr>
      <tr>
        <td>Contact Phone</td>
        <td>{{ performer.contact_phone }}</td>
      </tr>
    </tbody>
  </table>
  <p>
    <router-link class="btn btn-default" :to="{ name: 'performers_index' }">Cancel</router-link>
    <router-link class="btn btn-warning" :to="{ name: 'performers_edit', params: { id: performer._id }}">Edit</router-link>
    <button class="btn btn-danger" @click="destroy()">Delete</button>
  </p>
</b-col>
</template>

<script>
// import TodoItem from "./TodoItem"
import api from '@/api'

export default {
  name: 'PerformersIndex',
  components: {},
  data() {
    return {
      performer: {},
    }
  },
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
      console.log(this.$route.params.id);
      api.get(`/performers/${this.$route.params.id}`)
        .then(response => {
          console.log(response);
          this.performer = response.data
        })
        .catch(error => console.log(error))
    },
    destroy() {
      api.delete(`/performers/${this.$route.params.id}`)
        .then(response => {
          console.log(response);
          this.$router.push({
            name: 'performers_index'
          });
        })
        .catch(error => console.log(error))
    }
  }
};
</script>
