<template>
  <section class="talk">
    <h3 class="title"><u>Talk</u>: {{ title }}</h3>
    <div class="recording" v-if="recording">
      <iframe
        :src="recording"
        width="100%"
        height="100%"
        frameborder="0"
        allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
      />
    </div>
    <div v-if="description" v-html="description" class="description"></div>
    <EventSpeaker :speaker="speaker" :bio="bio" />
    <ItemRow v-if="deck">
      <Icon name="deck" slot="icon" />
      <a :href="deck" target="_blank">Speaker Deck</a>
    </ItemRow>
    <ItemRow v-if="issue">
      <Icon name="github" slot="icon" />
      <a :href="issue" target="_blank">{{ issue | filename }} </a>
    </ItemRow>
  </section>
</template>

<script>
export default {
  props: [
    "title",
    "description",
    "speaker",
    "bio",
    "deck",
    "issue",
    "recording"
  ],
  filters: {
    filename(value) {
      return value.split("/").pop();
    }
  }
};
</script>

<style scoped>
.talk {
  position: relative;
  border: 1px solid rgba(0, 0, 0, 0.05);
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 4px 10px -4px rgba(0, 0, 0, 0.5);
}

.recording {
  width: 100%;
  padding-top: 56.29%;
  position: relative;
}

.description {
  margin-bottom: 1rem;
}

iframe {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
</style>
