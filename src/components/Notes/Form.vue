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
      const note = { title: this.value, tags: this.tags.filter((tag) => tag.isActive) };
      this.$emit('onSubmit', note);
      this.value = '';
      const tags = this.tags.map((item) => {
        const tag = { ...item, isActive: false };
        return tag;
      });
      this.tags = tags;
    },
    handleTagClick(tag) {
      const currentTag = this.tags.find((tagItem) => tagItem.title === tag.title);
      currentTag.isActive = !currentTag.isActive;
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
