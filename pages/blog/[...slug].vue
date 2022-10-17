<template>
  <main>
    <ContentDoc v-slot="{ doc }">
      <h1>
        {{
          new Date(doc.date).toLocaleDateString("ru", {
            // weekday: "long",
            year: "numeric",
            month: "long",
            day: "numeric",
          })
        }}
      </h1>
      <ContentRenderer :value="doc" />
    </ContentDoc>
  </main>
</template>
