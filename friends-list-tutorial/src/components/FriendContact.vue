<template>
  <li>
    <h2>{{name}} {{isFavorite ? '(Fave)' : ''}}</h2>
    <button @click="toggleFavorite">Toggle Favorite</button>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
    <ul v-if="detailsAreVisible">
      <li><strong>Phone:</strong> {{phone}}</li>
      <li><strong>Email:</strong> {{email}}</li>
    </ul>
    <button @click="$emit('delete', id)">Delete</button>
  </li>
</template>

<script>
export default {
  emits: ['toggle-favorite', 'delete'],
  props: {
    name: {
      type: String,
      required: true,
    },
    email: {
      type: String,
      required: true
    },
    phone: {
      type: String,
      required: false,
      default: '-',
      validator: function(value) {
        return value.length >= 10 && value.length <= 13;
      }
    },
    id: {
      type: Number,
      required: true
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  data() {
    return {
      detailsAreVisible: false
    }
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite() {
      this.$emit('toggle-favorite', this.id);
    }
  }
};
</script>