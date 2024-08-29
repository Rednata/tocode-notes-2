<template>
  <Form @onSubmit="handlerSubmit"></Form>
  <List :items="notes" @onRemove="handleRemove"/>

</template>

<script>
import Form from '@/components/Notes/Form.vue';
import List from '@/components/Notes/List.vue';

export default {
  components: { Form, List },
  data() {
    return {
      notes: [
        {
          title: 'Learn Vue3',
          tags: ['work'],
        },
        {
          title: 'Finish Course',
          tags: ['work', 'home'],
        },
      ],
    };
  },
  mounted() {
    this.getNotes();
  },
  watch: {
    notes: {
      handler(updateList) {
        console.log('updateList: ', updateList);
        localStorage.setItem('notes', JSON.stringify(updateList));
      },
      deep: true,
    },
  },
  methods: {
    getNotes() {
      const localNotes = localStorage.getItem('notes');
      if (localNotes) {
        console.log('localNotes: ', localNotes);
        this.notes = JSON.parse(localNotes);
      }
    },
    handlerSubmit(title) {
      const note = { title, tags: [] };
      this.notes.push(note);
      console.log('this.notes: ', this.notes);
    },
    handleRemove(idx) {
      this.notes.splice(idx, 1);
    },
  },
};
</script>

<style lang="scss" scoped>

</style>
