<template>
  <div
    class="min-h-screen bg-slate-950 text-slate-100 px-4 sm:px-8 py-10 flex justify-center items-start"
  >
    <div class="w-full max-w-4xl">
      <div
        class="bg-slate-900 rounded-xl shadow-lg p-8 sm:p-10 border border-slate-800 space-y-10"
      >
        <h1 class="text-3xl sm:text-4xl font-bold text-center text-slate-100">
          🧠 Trader Patience Toolkit
        </h1>

        <section class="space-y-4">
          <h2 class="text-xl sm:text-2xl font-semibold text-slate-200">
            🧾 If-Then Rules
          </h2>
          <ul class="space-y-2 list-decimal pl-6 text-base text-slate-300">
            <li v-for="(rule, i) in ifThenRules" :key="i">{{ rule }}</li>
          </ul>
          <div class="flex flex-col gap-3 sm:flex-row">
            <input
              v-model="newRule"
              placeholder="If SPY... then I will..."
              class="flex-1 p-3 rounded-md border border-slate-700 bg-slate-800 text-slate-100 focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <button
              @click="addRule"
              class="bg-blue-600 text-white px-5 py-3 rounded-md hover:bg-blue-700 transition"
            >
              Add Rule
            </button>
          </div>
        </section>

        <section class="space-y-4">
          <h2 class="text-xl sm:text-2xl font-semibold text-slate-200">
            ⏱️ 2-Minute Rule
          </h2>
          <p class="text-base text-slate-400">
            Pause and observe 2 candles before entering. Let the setup confirm —
            reduce impulses.
          </p>
        </section>
        <section class="space-y-4">
          <h2 class="text-xl sm:text-2xl font-semibold text-slate-200">
            📋 Trade Scorecard
          </h2>
          <div class="space-y-3">
            <div
              v-for="(item, index) in scorecard"
              :key="index"
              class="flex justify-between items-center bg-slate-800 border border-slate-700 p-4 rounded-md"
            >
              <span class="text-base text-slate-300">{{ item.label }}</span>
              <button
                @click="item.checked = !item.checked"
                :class="
                  item.checked
                    ? 'bg-green-600 hover:bg-green-700'
                    : 'bg-slate-700 hover:bg-slate-600'
                "
                class="text-white px-4 py-2 rounded-md transition"
              >
                {{ item.checked ? "Checked" : "Mark" }}
              </button>
            </div>
          </div>
          <p class="pt-2 text-base font-medium text-slate-300">
            Checklist Score: {{ checkedScore }}/{{ scorecard.length }}
          </p>
        </section>
        <section class="space-y-4">
          <h2 class="text-xl sm:text-2xl font-semibold text-slate-200">
            📓 Non-Trade Journal
          </h2>
          <ul class="space-y-2 list-decimal pl-6 text-base text-slate-300">
            <li v-for="(note, i) in journalNotes" :key="i">{{ note }}</li>
          </ul>
          <div class="flex flex-col gap-3 sm:flex-row">
            <input
              v-model="newNote"
              placeholder="If SPY... then I will..."
              class="flex-1 p-3 rounded-md border border-slate-700 bg-slate-800 text-slate-100 focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <button
              @click="addNote"
              class="mt-3 bg-blue-600 text-white px-5 py-3 rounded-md hover:bg-blue-700 transition"
            >
              Add Note
            </button>
          </div>
        </section>

       
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const ifThenRules = ref([]);
const newRule = ref("");
const addRule = () => {
  if (newRule.value.trim()) {
    ifThenRules.value.push(newRule.value.trim());
    newRule.value = "";
  }
};

const journalNotes = ref([]);
const newNote = ref("");
const addNote = () => {
  if (newNote.value.trim()) {
    journalNotes.value.push(newNote.value.trim());
    newNote.value = "";
  }
};

const scorecard = ref([
  { label: "Clean price structure", checked: false },
  { label: "Near key EMA", checked: false },
  { label: "Volume confirmation", checked: false },
  { label: "MACD/RSI supports", checked: false },
  { label: "Pre-planned setup", checked: false },
]);

const checkedScore = computed(() => {
  return scorecard.value.filter((item) => item.checked).length;
});
</script>

<style>
body {
  padding: 10;
  font-family: system-ui, sans-serif;
  background-color: #0f172a;
}
.flex.flex-col.gap-3.sm\:flex-row {
  margin: 35px;
}
button.bg-blue-600.text-white.px-5.py-3.rounded-md.hover\:bg-blue-700.transition {
  margin-top: 20px;
}
p.text-base.text-slate-400 {
  margin: 35px;
}
.flex.justify-between.items-center.bg-slate-800.border.border-slate-700.p-4.rounded-md {
    margin: 10px 35px;
    border-style: none;
}
input.flex-1.p-3.rounded-md.border.border-slate-700.bg-slate-800.text-slate-100.focus\:outline-none.focus\:ring-2.focus\:ring-blue-500 {
  border-radius: 5px;
  padding: 20px 10px;
}
li{
  text-align: left;
}
</style>
