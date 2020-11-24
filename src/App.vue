<template>
  <section class="container">
    <div class="wrapper">
      <div>
        <label class="input-label" :class="activeClass">
          <input type="file" class="input-file" @change="handlerChange" />
          {{ label }}
        </label>
        <p class="input-sublabel">{{ sublabel }}</p>
      </div>
      <p class="default-text" :class="statusText">{{ check }}</p>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      activeClass: "default",
      label: "Загрузить скан страницы с фотографией",
      sublabel: "Размер файла не более 5мб",
      check: "",
      statusText: "",
    };
  },
  methods: {
    handlerChange(event) {
      this.activeClass = "load";
      const e = event.target.files[0];
      const name = e.name;
      const size = "(" + (e.size / 1024).toFixed(2) + " Кб)";
      setTimeout(() => {
        this.activeClass = "checked";
        this.sublabel = name + " " + size;
        this.statusText = "";
        this.check = "Проверка...";
        setTimeout(() => {
          if (Math.random() <= 0.5) {
            this.activeClass = "accept";
            this.statusText = "accept-text";
            this.label = "Страница с пропиской";
            this.check = "Проверенно";
          } else {
            this.activeClass = "denied";
            this.statusText = "denied-text";
            this.label = "Загрузить скан страницы с фотографией";
            this.check = "Отклоненно";
            this.sublabel = "Размер файла не более 5мб";
          }
        }, 2000);
      }, 2000);
    },
  },
};
</script>
