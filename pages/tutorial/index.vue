<template>
  <Head>
    <Title>ProDoc - Tutorial</Title>
    <link rel="shortcut icon" href="logo.ico" type="image/x-icon">
  </Head>
  <NuxtLayout name="docs" :data="data"> </NuxtLayout>
</template>

<script lang="ts">
export default {
  data() {
    return {
      data: {
        title: "ProDoc",
        description: "Create your own documentation in ProDoc",
        back_arrow: true,
        back_arrow_link: "/build",
        components: [
          {
            type: "image",
            src: "preview.png",
          },
          {
            type: "text",
            title: false,
            text: "This is the Prewiew of your documentation. It updates live as you edit.",
          },
          {
            type: "space",
          },
          {
            type: "image",
            src: "edit.png",
          },
          {
            type: "text",
            title: false,
            text: "Next we have the work area.",
          },
          {
            type: "space",
          },
          {
            type: "image",
            src: "title+desc.png",
          },
          {
            type: "text",
            title: false,
            text: "In there we have the Title/Description editor.",
          },
          {
            type: "space",
          },
          {
            type: "image",
            src: "toolbar.png",
          },
          {
            type: "text",
            title: false,
            text: "Down there whe have the Toolbar for Dark/Light Mode, Add Text, Add Image, Add List, Add Space, Edit Data and Clear all.",
          },
          {
            type: "space",
          },
          {
            type: "image",
            src: "listView.png",
          },
          {
            type: "text",
            title: false,
            text: "Finally we get to the list view where all your elements are listed. You can drag them or click on the up/down arrows to reorganize them. Edit the src, text and items (of list) down in the input box/item view. To delete items click on the red delete button.",
          },
          {
            type: "space",
          },
          {
            type: "image",
            src: "dark.png",
          },
          {
            type: "text",
            title: false,
            text: "Btw we have a darkmode too (:",
          },
        ],
      },
    };
  },
};
</script>

<style>
/*  */
</style>