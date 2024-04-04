<script setup>
import { ref, unref } from 'vue';
import { Switch, SwitchGroup, SwitchLabel } from '@headlessui/vue'

const password = ref('HG!ok876@45');
const passwordLength = ref(12);
// const types = ref(["lowercase"]);

const uppercaseSelected = ref(false);
const lowercaseSelected = ref(true);
const numbersSelected = ref(false);
const symbolsSelected = ref(false);

const types = {
  uppercase: false,
  lowercase: true,
  numbers: false,
  symbols: false
};

const characters = {
  uppercase: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
  lowercase: "abcdefghijklmnopqrstuvwxyz",
  numbers: "0123456789",
  symbols: "!@#$%^&*()_+~`|}{[]:;?><,./-="
};

function checkOptions() {

  console.log('testing', types);
}

function generatePassword() {
  let selectedCharacters = "";
  let generatedPassword = "";

  Object.keys(types).forEach((option) => {
    if (types[option]) {
      selectedCharacters += characters[option];
    }
  });

  // debugger

  for (let i = 0; i < passwordLength.value; i++) {
    generatedPassword += selectedCharacters.charAt(
      Math.floor(Math.random() * selectedCharacters.length)
    );
  }

  password.value = generatedPassword;
}

function copyPassword() {
  navigator.clipboard.writeText(password.value);
}

/**
 * TODO: Add validation to check if password is more than 12 characters
 * and has at least two checkboxes selected
 * if not change color of panel to oranage
 */

</script>

<template>
  <div class="project | ">
    <div class="container">
      <div class="panel | relative bg-white px-6 pt-10 pb-8 shadow-xl ring-1 ring-gray-900/5 rounded-lg divide-y divide-red-300/50">
        <div class="password-area pb-6">
          <h3 class="password-box | bg-slate-100 p-4 flex justify-center items-center mb-4 text-3xl font-medium">{{ password }}</h3>
          <div class="button-group | flex gap-4">
            <button type="button"
                    class="copy-btn | btn-base btn btn-copy-theme-color"
                    @click="copyPassword()">
              <!-- <BeakerIcon class="-ml-0.5 h-5 w-5"
                          aria-hidden="true" /> -->
              Copy Password
            </button>
            <button type="button"
                    class="reset-btn | btn-base btn btn-reset-theme-color"
                    @click="">
              <!-- <BeakerIcon class="-ml-0.5 h-5 w-5"
                          aria-hidden="true" /> -->
              Reset Password
            </button>
          </div>
        </div>
        <div class="form-area | pt-8">
          <!-- toggles -->
          <div class="type-selections | grid grid-cols-1 gap-4 space-y-2">
            <SwitchGroup as="div"
                         class="uppercase-selelction flex items-center">
              <Switch v-model="types.uppercase"
                      value="true"
                      :class="[uppercaseSelected
            ? 'bg-indigo-600'
            : 'bg-gray-200'
            , 'relative inline-flex h-6 w-11 flex-shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-offset-2'
          ]"
                      @click="types.uppercase = !types.uppercase; uppercaseSelected = !uppercaseSelected; checkOptions()">
                <span aria-hidden="true"
                      :class="[uppercaseSelected ? 'translate-x-5' : 'translate-x-0', 'pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow ring-0 transition duration-200 ease-in-out']" />
              </Switch>
              <SwitchLabel as="span"
                           class="ml-3 text-sm">
                <span class="font-medium text-gray-900">Uppercase</span>
              </SwitchLabel>
            </SwitchGroup>
            <SwitchGroup as="div"
                         class="lowercase-selelction flex items-center">
              <Switch v-model="types.lowercase"
                      value="true"
                      :class="[lowercaseSelected
            ? 'bg-indigo-600'
            : 'bg-gray-200'
            , 'relative inline-flex h-6 w-11 flex-shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-offset-2'
          ]"
                      @click="types.lowercase = !types.lowercase; lowercaseSelected = !lowercaseSelected; checkOptions()">
                <span aria-hidden="true"
                      :class="[lowercaseSelected ? 'translate-x-5' : 'translate-x-0', 'pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow ring-0 transition duration-200 ease-in-out']" />
              </Switch>
              <SwitchLabel as="span"
                           class="ml-3 text-sm">
                <span class="font-medium text-gray-900">Lowercase</span>
              </SwitchLabel>
            </SwitchGroup>
            <SwitchGroup as="div"
                         class="numbers-selelction flex items-center">
              <Switch v-model="types.numbers"
                      value="true"
                      :class="[numbersSelected
            ? 'bg-indigo-600'
            : 'bg-gray-200'
            , 'relative inline-flex h-6 w-11 flex-shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-offset-2'
          ]"
                      @click="types.numbers = !types.numbers; numbersSelected = !numbersSelected; checkOptions()">
                <span aria-hidden="true"
                      :class="[numbersSelected ? 'translate-x-5' : 'translate-x-0', 'pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow ring-0 transition duration-200 ease-in-out']" />
              </Switch>
              <SwitchLabel as="span"
                           class="ml-3 text-sm">
                <span class="font-medium text-gray-900">Numbers</span>
                {{ ' ' }}
                <span class="text-gray-500">(ex. 0-9)</span>
              </SwitchLabel>
            </SwitchGroup>
            <SwitchGroup as="div"
                         class="symbols-selelction flex items-center">
              <Switch v-model="types.symbols"
                      value="true"
                      :class="[symbolsSelected
            ? 'bg-indigo-600'
            : 'bg-gray-200'
            , 'relative inline-flex h-6 w-11 flex-shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-offset-2'
          ]"
                      @click="types.symbols = !types.symbols; symbolsSelected = !symbolsSelected; checkOptions()">
                <span aria-hidden="true"
                      :class="[symbolsSelected ? 'translate-x-5' : 'translate-x-0', 'pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow ring-0 transition duration-200 ease-in-out']" />
              </Switch>
              <SwitchLabel as="span"
                           class="ml-3 text-sm">
                <span class="font-medium text-gray-900">Symbols</span>
                {{ ' ' }}
                <span class="text-gray-500">(ex. !@#$%^)</span>
              </SwitchLabel>
            </SwitchGroup>
          </div>
          <div class="password-length | flex gap-4 items-center mb-8 mt-2">
            <div class="length-value text-2xl">{{ passwordLength }}</div>
            <div class="mt-4">
              <h3>Password Length</h3>
              <input type="range"
                     name=""
                     min="6"
                     max="32"
                     value="12"
                     id="password_length"
                     v-model="passwordLength">
            </div>
          </div>
          <div>
            <button class="generate-btn | btn btn-base btn btn-generate-theme-color btn-full"
                    @click.prevent="generatePassword()">Generate Password</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  @apply relative flex flex-col items-center justify-center min-h-screen overflow-hidden w-full mx-auto py-6 sm:py-12
}
</style>
