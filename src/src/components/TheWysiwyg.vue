<template>
  <div class="wysiwyg">
    <div class="wysiwyg__controls">
      <div class="wysiwyg__button" @click="back">
        <icon-back />
      </div>
      <div class="wysiwyg__button" @click="next">
        <icon-next />
      </div>
      <div class="wysiwyg__button" @mousedown="title">
        <icon-title />
      </div>
      <div class="wysiwyg__button" @mousedown="paragraph">
        <icon-paragraph />
      </div>
      <div class="wysiwyg__button" @mousedown="picture">
        <icon-picture />
      </div>
      <div class="wysiwyg__copy" @click="html">Скопировать HTML</div>
    </div>
    <div
      ref="wysiwyg"
      class="wysiwyg__content"
      contenteditable="true"
      placeholder="Введите текст"
      @paste="paste"
    >
      <div>
        Таким образом консультация с широким активом представляет собой
        интересный эксперимент проверки позиций, занимаемых участниками в
        отношении поставленных задач. С другой стороны постоянное
        информационно-пропагандистское обеспечение нашей деятельности
        представляет собой интересный эксперимент проверки форм развития.
        Идейные соображения высшего порядка, а также укрепление и развитие
        структуры влечет за собой процесс внедрения и модернизации
        соответствующий условий активизации. Задача организации, в особенности
        же реализация намеченных плановых заданий играет важную роль в
        формировании дальнейших направлений развития. Повседневная практика
        показывает, что постоянное информационно-пропагандистское обеспечение
        нашей деятельности играет важную роль в формировании существенных
        финансовых и административных условий.
      </div>
      <div class="wysiwyg__space"></div>
      <div>
        <font size="6">Смотрите какие обезьянки</font>
      </div>
      <div class="wysiwyg__space"></div>
      <div>
        <img src="../assets/img/default.jpg" />
      </div>
      <div class="wysiwyg__space"></div>
      <div>
        Таким образом консультация с широким активом представляет собой
        интересный эксперимент проверки позиций, занимаемых участниками в
        отношении поставленных задач. С другой стороны постоянное
        информационно-пропагандистское обеспечение нашей деятельности
        представляет собой инйцу шо шщйоц ущойц ущошцщйуо йцщуо йщцоу щйоу
        шщйцош ущйтересный эксперимент проверки форм развития. Идейные
        соображения высшего порядка, а также укрепление и развитие структуры
        влечет за собой процесс внедрения и модернизации соответствующий условий
        активизации. Задача организации, в особенности же реализация намеченных
        плановых заданий играет важную роль в формировании дальнейших
        направлений развития. Повседневная практика показывает, что постоянное
        информационно-пропагандистское обеспечение нашей деятельности играет
        важную роль в формировании существенных финансовых и административных
        условий.
      </div>
      <div class="wysiwyg__space"></div>
      <div>
        Товарищи! новая модель организационной деятельности требуют от нас
        анализа направлений прогрессивного развития. Задача организации, в
        особенности же постоянный количественный рост и сфера нашей активности
        требуют от нас анализа позиций, занимаемых участниками в отношении
        поставленных задач. Задача организации, в особенности же реализация
        намеченных плановых заданий требуют от нас анализа системы обучения
        кадров, соответствует насущным потребностям.
      </div>
    </div>
  </div>
</template>

<script>
import IconBack from "@/assets/icons/IconBack.vue";
import IconNext from "@/assets/icons/IconNext.vue";
import IconParagraph from "@/assets/icons/IconParagraph.vue";
import IconPicture from "@/assets/icons/IconPicture.vue";
import IconTitle from "@/assets/icons/IconTitle.vue";

export default {
  name: "WYSIWYG",
  components: {
    IconBack,
    IconNext,
    IconParagraph,
    IconPicture,
    IconTitle,
  },
  methods: {
    escapeText(text) {
      var map = {
        "&": "&amp;",
        "<": "&lt;",
        ">": "&gt;",
        '"': "&quot;",
        "'": "&#039;",
      };
      return text.replace(/[&<>"']/g, function (m) {
        return map[m];
      });
    },
    paste(e) {
      e.preventDefault();
      const text = (e.originalEvent || e).clipboardData.getData("text/plain");
      document.execCommand("insertHtml", false, this.escapeText(text));
    },
    back() {
      document.execCommand("undo", false, null);
    },
    next() {
      document.execCommand("redo", false, null);
    },
    picture() {
      let url = prompt("Введите адрес картинки", "");
      document.execCommand("insertImage", false, url);
    },
    title() {
      document.execCommand("fontSize", false, "6");
    },
    paragraph() {
      document.execCommand(
        "insertHTML",
        false,
        '</div><div class="wysiwyg__space"></div><div>' +
          document.getSelection().toString() +
          '</div><div class="wysiwyg__space"></div><div>'
      );
    },
    html() {
      const wysiwyg = this.$refs.wysiwyg;
      navigator.clipboard.writeText(wysiwyg.outerHTML);
    },
  },
};
</script>

<style lang="scss">
.wysiwyg {
  padding: 77px 107px;
  height: 100%;
  @media (max-width: 750px) {
    padding: 30px;
  }
  &__space {
    height: 20px;
    width: 100%;
  }
  &__content {
    border: none;
    outline: none;
    color: #eaeaea;
    font-size: 15px;
    height: inherit;
    width: 100%;
    padding-bottom: 30px;
    overflow-y: auto;
    overflow-x: hidden;
    -ms-overflow-style: none;
    scrollbar-width: none;
    img {
      max-width: 100%;
      height: auto;
    }
    &::-webkit-scrollbar {
      width: 0;
      height: 0;
    }
    &:empty {
      &:before {
        content: attr(placeholder);
        color: #555;
      }
    }
  }
  &__controls {
    display: flex;
    align-items: center;
    color: #639eff;
    font-size: 15px;
    margin-bottom: 31px;
    @media (max-width: 750px) {
      flex-wrap: wrap;
    }
  }
  &__copy {
    cursor: pointer;
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    @media (max-width: 456px) {
      margin-top: 20px;
    }
    &:hover {
      color: #fff;
    }
    &:active {
      transform: scale(0.98);
    }
  }
  &__button {
    width: 42px;
    height: 38px;
    cursor: pointer;
    border-radius: 4px;
    background: #282828;
    transition: all 0.3s ease;
    margin-right: 12px;
    display: flex;
    justify-content: center;
    align-items: center;
    @media(max-width: 750px) {
      margin-right: 10px;
    }
    svg {
      pointer-events: none;
    }
    &:hover {
      color: #fff;
    }
    &:active {
      transform: scale(0.9);
    }
  }
}
</style>
