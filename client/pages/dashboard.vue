<template>
  <div>
    <p>Users List</p>

    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
          <th>Action</th> <!-- Added Action column header -->
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in data.users" :key="user.id">
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>
            <!-- Added delete button -->
            <button @click="deleteUser(user.id)" class="action-btn delete">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  async setup() {
    const data = ref(null);

    // Check if user is logged in on component mount
    onMounted(() => {
      checkLogged();
    });

    async function checkLogged() {
      if (!localStorage.getItem('_token')) {
          console.log('no token');
      }
    }

    async function deleteUser(userId) {
      try {
        console.log('Deleting user with ID:', userId);
      } catch (error) {
        console.error('Error deleting user:', error);
    
      }
    }

    try {
      const { data } = await useFetch('http://127.0.0.1:8000/api/getUsers/'); 
      return { data, deleteUser };
    } catch (error) {
      console.error('Error fetching users:', error);
      // You might want to handle errors more gracefully, for example by showing an error message to the user
    }
  },
};
</script>

<style scoped>
/* Add your table styles here if needed */
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

.action-btn {
  margin-right: 5px;
  padding: 3px 8px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
}

.view {
  background-color: green;
  color: white;
}

.edit {
  background-color: yellow;
  color: #333;
}

.delete {
  background-color: red;
  color: white;
}
</style>
