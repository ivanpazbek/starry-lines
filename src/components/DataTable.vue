<template>
  <div class="w-full mb-6 md:mb-0">
    <div class="relative  mb-4">
      <div class="usage-filter">
      <label class="filter-label">Usage Filter</label>
      <select
        @change="filterData(subCat)"
        v-model="subCat"
        class="
          block
          appearance-none
          bg-gray-200
          border border-gray-200
          text-gray-700
          py-3
          px-4
          pr-8
          rounded
          leading-tight
          focus:outline-none focus:bg-white focus:border-gray-500
        "
        id="grid-state"
      >
        <option value="">Sub filter</option>
        <option value="app">App</option>
        <option value="article">Article</option>
        <option value="api">Api</option>
      </select>
      </div>
      <div
        class="
          pointer-events-none
          absolute
          inset-y-0
          right-0
          flex
          items-center
          px-2
          text-gray-700
        "
      >
        <svg
          class="fill-current h-4 w-4"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 20 20"
        >
          <path
            d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
          />
        </svg>
      </div>
    </div>
  </div>
  <EasyDataTable
  ref="data-table"
  table-class-name="data-table"
  class="font-mono"
  :headers="headers"
  :items="items"
  :loading="loading"
  :header-item-class-name="getHeaderClassNameByIndex"
  :body-item-class-name="getItemClassNameByIndex"
  updatePage
  @click-row="expandRow"
  theme-color="#FFC40C"
  header-text-direction="center"
  body-text-direction="center"
  alternating
>
  <template #item-name="{ name, url }">
    <a
      class="repo-link after:content-['_↗'] after:text-sm after:pb-2"
      :href="url"
      target="_blank"
      rel="noopener noreferrer"
      >{{ name }}</a
    >
  </template>
  <template #expand="item">
    <div class="p-5">
      <h2 class="font-bold">Short Descriptions</h2>
      <p v-if="!item.short_description">None 😢</p>
      <p v-else>{{ item.short_description }}</p>
    </div>
  </template>
</EasyDataTable>
</template>

<style>
.sortable.none .sortType-icon {
  display: none !important;
}

.previous-page__click-button.first-page .arrow,
.next-page__click-button.last-page .arrow {
  border-color: black !important;
}

.easy-data-table__rows-selector ul.select-items li.selected {
  color: black !important;
}

.previous-page__click-button .arrow,
.next-page__click-button .arrow {
  border-color: white !important;
}

.data-table {
  --easy-table-border: 1px solid #445269;
  --easy-table-row-border: 1px solid #445269;

  --easy-table-header-font-size: 14px;
  --easy-table-header-height: 50px;
  --easy-table-header-font-color: #ffc40c;
  --easy-table-header-background-color: #0c173c;

  --easy-table-header-item-padding: 10px 15px;

  --easy-table-body-even-row-font-color: #fff;
  --easy-table-body-even-row-background-color: #4c5d7a;

  --easy-table-body-row-font-color: #c0c7d2;
  --easy-table-body-row-background-color: #0c173c;
  --easy-table-body-row-height: 50px;
  --easy-table-body-row-font-size: 14px;

  --easy-table-body-row-hover-font-color: #0c173c;
  --easy-table-body-row-hover-background-color: #eee;

  --easy-table-body-item-padding: 10px 15px;

  --easy-table-footer-background-color: #0c173c;
  --easy-table-footer-font-color: #c0c7d2;
  --easy-table-footer-font-size: 14px;
  --easy-table-footer-padding: 0px 10px;
  --easy-table-footer-height: 50px;

  --easy-table-rows-per-page-selector-width: 70px;
  --easy-table-rows-per-page-selector-option-padding: 10px;

  --easy-table-scrollbar-track-color: #0c173c;
  --easy-table-scrollbar-color: #0c173c;
  --easy-table-scrollbar-thumb-color: #4c5d7a;
  --easy-table-scrollbar-corner-color: #0c173c;

  --easy-table-loading-mask-background-color: #0c173c;
}
.usage-filter {
  display: flex;
  justify-content: center;
}

.usage-filter .filter-label {
  color: wheat;
  margin-top: 10px;
  margin-right: 30px;
  vertical-align: middle;
}
thead.vue3-easy-data-table__header tr th:nth-child(2) > span {
  justify-content: left !important;
}
</style>

<script lang="ts">
import { defineComponent } from "vue";
import Vue3EasyDataTable, { Header } from "vue3-easy-data-table";
import type { ClickRowArgument } from "vue3-easy-data-table";
import "vue3-easy-data-table/dist/style.css";

const HEADER_REACTIVE_CLASSES: any = {
  expand: "!px-0 sm:px-0",
  rank: "!pl-2 !pr-0 sm:!px-3 text-0 before:content-['#'] before:inline before:text-lg sm:text-base sm:before:content-none",
  name: "text-lg sm:text-xl",
  updatedAt: "hidden md:table-cell",
  createdAt: "hidden lg:table-cell",
  stargazers:
    "text-0 before:content-['★'] before:inline before:text-2xl sm:text-base sm:before:content-none",
  loc: "text-0 before:content-['LoC'] before:inline before:text-lg sm:text-base sm:before:content-none",
  score: "text-lg sm:text-xl",
  all: "break-words sm:text-lg lg:text-xl text-black",
};

const REACTIVE_CLASSES: any = {
  expand: "expand-button !px-0 sm:!px-3",
  rank: "repo-rank !pl-2 !pr-0 sm:!px-3",
  name: "break-all text-ellipsis",
  updatedAt: "hidden md:table-cell",
  createdAt: "hidden lg:table-cell",
  all: "text-sm sm:text-lg",
};

export default defineComponent({
  props: {
    category: {
      type: String,
      required: true,
    },
  },
  components: {
    EasyDataTable: Vue3EasyDataTable,
  },
  data() {
    return {
      headers: [
        {
          text: "",
          value: "",
          sortable: true,
        },
      ],
      colms: [],
      rows: [],
      items: [{
        usage:''
      }],
      mainData: [{
        usage:''
      }],
      subCat: "",
      loading: true,
    };
  },
  methods: {
    filterData(subCat: String) {
      this.items = this.mainData;
      if (subCat != "")
        this.items = this.items.filter((item) => item.usage == subCat);
    },
    async fetchData() {
      this.loading = true;
      this.mainData = [];

      var self = this;
      let url = "https://docs.google.com/spreadsheets/d/";
      let sheet_id = "1fBeVohwepL7xSBq1U9-xogPfReSJo2JptTkF5yeXfB4";
      let query1 = "/gviz/tq";
      let endpoint = `${url}${sheet_id}${query1}`;
      await fetch(endpoint)
        .then((res) => res.text())
        .then((data) => {
          const temp = data.substring(47).slice(0, -2);
          const json = JSON.parse(temp);
          self.colms = json.table.rows[0].c.map((col: { v: String }) => {
            return col.v;
          });

          json.table.rows.forEach((row: {c: any[];},index: Number) => {
              if (index != 0) {
                var obj:any = {
                  address: "",
                  category: "",
                  content: "",
                  keyword_1: "",
                  keyword_2: "",
                  keyword_3: "",
                  name: "",
                  short_description: "",
                  usage: "",
                };

                row.c.map((value: {v: String},key: any) => {
                    if(self.colms[key]=='category' || self.colms[key]=='usage')
                    obj[self.colms[key]] = value.v.toLowerCase().trim();
                    else
                    obj[self.colms[key]] = value.v;
                  });

                if(self.category=='') self.mainData.push(obj);
                else if (self.category!='' && obj.category.trim() == self.category) self.mainData.push(obj);
                
              }
            }
          );
        });
      this.items = self.mainData;
      this.loading = false;
    },
    expandRow(item: ClickRowArgument) {
      let xpath = `//tr[td[text()='${item["rank"]}'][contains(@class, 'repo-rank')]]/td[contains(@class, 'expand-button')]`;
      let expandButton = document.evaluate(
        xpath,
        document,
        null,
        XPathResult.FIRST_ORDERED_NODE_TYPE,
        null
      ).singleNodeValue as HTMLElement;
      expandButton.click();
    },
    async shrinkAllRows() {
      let expandButtons = document.querySelectorAll(
        ".expanding"
      ) as NodeListOf<HTMLElement>;
      expandButtons.forEach((button) => {
        button.click();
      });
    },
    getHeaderClassNameByIndex(header: Header, index: string) {
      return (
        HEADER_REACTIVE_CLASSES.all +
        " " +
        HEADER_REACTIVE_CLASSES[header.value]
      );
    },
    getItemClassNameByIndex(column: string, rowNumber: number) {
      return REACTIVE_CLASSES.all + " " + REACTIVE_CLASSES[column];
    },
    getFlagEmoji(countryCode: string) {
      if (countryCode == undefined) return;
      if (countryCode == "ZH") countryCode = "CN";
      if (countryCode == "JA") countryCode = "JP";
      const codePoints = countryCode
        .toUpperCase()
        .split("")
        .map((char) => 127397 + char.charCodeAt(0));
      return (
        String.fromCodePoint(codePoints[0]) +
        String.fromCodePoint(codePoints[1])
      );
    },
  },
  mounted() {
    this.headers = [
      {
        text: "Name",
        value: "name",
        sortable: true,
      },
      {
        text: "Category",
        value: "category",
        sortable: true,
      },
      {
        text: "Usage",
        value: "usage",
        sortable: true,
      },
      {
        text: "Content",
        value: "content",
        sortable: true,
      },
      {
        text: "Keword 1",
        value: "keyword_1",
        sortable: true,
      },
      {
        text: "Keword 2",
        value: "keyword_2",
        sortable: true,
      },
      {
        text: "Keword 3",
        value: "keyword_3",
        sortable: true,
      },
      {
        text: "Address",
        value: "address",
        sortable: true,
      },
    ];
    this.fetchData();
  },
  watch: {
    category() {
      this.subCat = "";
      this.shrinkAllRows();
      this.fetchData();
      (this.$refs["data-table"] as any).updatePage(1);
    },
  },
  updated() {
    Array.from(document.getElementsByClassName("repo-link")).forEach(function (
      el
    ) {
      el.addEventListener("click", (e) => {
        e.stopPropagation();
      });
    });
  },
});
</script>
