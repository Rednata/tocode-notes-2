<template>
  <div class="note-form__wrapper">
    <form class="note-form" @submit.prevent="onSubmit">
      <label for="value">
        <textarea
        class=""
        type="text" required
        v-model="value"
        placeholder="Enter Your note">
        </textarea>
      </label>

      <button class="btn btnPrimary" type="submit">Add new note</button>
    </form>
    <TagsList :items="tags" @onItemClick="handleTagClick"/>
  </div>

</template>

<script>
import TagsList from '@/components/Notes/UI/TagsList.vue';

export default {
  components: { TagsList },
  data() {
    return {
      value: '',
      tags: [
        { title: 'home', isActive: false },
        { title: 'work', isActive: false },
        { title: 'travel', isActive: false },
      ],
    };
  },
  methods: {
    onSubmit() {
      this.$emit('onSubmit', this.value);
      console.log(this.value);
      this.value = '';
    },
    handleTagClick(tag) {
      console.log('tag: ', tag);
    },
  },
};
</script>

<style lang="scss" scoped>
.note-form__wrapper {
  display: flex;
  flex-direction: column;
  align-items: center
}
  .note-form {
    display: flex;
    flex-direction: column;
    max-width: 600px;
    width: 100%;

    textarea {
      margin-bottom: 0;
    }
  }
</style>
