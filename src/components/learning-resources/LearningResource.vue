<template>
  <li>
    <base-card>
      <header>
        <h3>{{ title }}</h3>
        <base-button @click="removeResources(id)" mode="flat">Delete</base-button>
      </header>
    <p>{{ description }}</p>
    <nav>
      <a :href="link">View Resource</a>
    </nav>
    </base-card>
  </li>
</template>
<script>
export default {
  // props: ['title', 'description', 'link', 'id']
  props: {
    title: {
      type: String,
      required: true,
      validator(value) {
        if (!value) {
          console.warn('`title` field cannot be empty.');
          return false;
        }
        return true;
      },
    },
    description: {
      type: String,
      required: true,
      validator(value) {
        if (!value) {
          console.warn('`description` field cannot be empty.');
          return false;
        }
        return true;
      },
    },
    link: {
      type: String,
      required: true,
      validator(value) {
        if (!value) {
          console.warn('`link` field cannot be empty.');
          return false;
        } else if (
          value.startsWith('https') ||
          value.startsWith('http') ||
          value.startsWith('/')
        ) {
          return true;
        }
        return false;
      },
    },
    id: {
      type: String,
      required: true,
    }
  },
  inject: ['removeResources']
};
</script>
<style scoped>
li {
  margin: auto;
  max-width: 30rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>