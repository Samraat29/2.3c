<template>
  <div>
    <!-- Template Syntax -->
    <div class="output">
      <p>{{ message }}</p>
      <div v-html="rawHTML"></div>
      <input :id="inputId" />
      <p>{{ uppercaseMessage() }}</p>
    </div>

    <!-- Class and Style Bindings -->
    <div class="output">
      <div :class="{ 'active': isActive, 'error': hasError }">Class Binding Example</div>
      <div :style="{ 'color': textColor, 'font-size': fontSize + 'px' }">Style Binding Example</div>
    </div>

    <!-- Event Handling -->
    <div class="output">
      <button @click="handleClickInline">Click Me (Inline)</button>
      <button @click="handleClickMethod">Click Me (Method)</button>
    </div>

    <!-- Computed Properties -->
    <div class="output">
      <p>Computed Property: {{ computedProperty }}</p>
    </div>

    <!-- Form Input Bindings -->
    <div class="output">
      <input type="text" v-model="textValue" />
      <p>Text Value: {{ textValue }}</p>

      <textarea v-model="trimmedTextValue"></textarea>
      <p>Trimmed Text Value: {{ trimmedTextValue }}</p>

      <!-- Single radio button -->
      <input type="radio" value="option1" v-model="radioValue" name="radioGroup" />
      <p>Radio Value: {{ radioValue }}</p>

      <select v-model="selectedOption">
        <option value="option1">Option 1</option>
        <option value="option2">Option 2</option>
      </select>
      <p>Selected Option: {{ selectedOption }}</p>

      <input type="number" v-model.number="numericValue" />
      <p>Numeric Value: {{ numericValue }}</p>
    </div>

    <!-- Reactivity Fundamentals -->
    <div class="output">
      <p>{{ count }}</p>
      <button @click="incrementCount">Increment Count</button>
    </div>

    <!-- List Rendering -->
    <div class="output">
      <ul>
        <li v-for="(value, key) in myObject" :key="key">
          {{ key }}: {{ value }}
        </li>
      </ul>

      <ul>
        <li v-for="n in 5" :key="n">{{ n }}</li>
      </ul>

      <ul>
        <template v-for="item in items" :key="item.id">
          <li>{{ item.name }}</li>
        </template>
      </ul>

      <ul>
        <li v-for="item in filteredItems" :key="item.id">
          {{ item.name }}
        </li>
      </ul>
    </div>

    <!-- Toggle Text -->
    <div class="output">
      <button @click="toggleText">Toggle Text</button>
      <p v-if="isTextVisible">This is some text!</p>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    // Template Syntax
    const message = ref('!@#$%^&*');
    const rawHTML = '<span style="color: red;">Raw HTML</span>';
    const inputId = 'my-input';

    // Computed Properties
    const inputValue = ref('Hello, 2.3!!!!!');
    const computedProperty = computed(() => inputValue.value.toUpperCase());

    // Reactivity Fundamentals
    const count = ref(0);

    // Form Input Bindings
    const textValue = ref('');
    const trimmedTextValue = ref('');
    const radioValue = ref('');
    const selectedOption = ref('option2');
    const numericValue = ref(0);

    // Class and Style Bindings
    const isActive = ref(true);
    const hasError = ref(false);
    const textColor = ref('red');
    const fontSize = ref(16);

    // Methods
    const uppercaseMessage = () => {
      return message.value.toUpperCase();
    };

    const handleClickInline = () => {
      alert('Inline Clicked');
    };

    const handleClickMethod = () => {
      alert('Method Clicked');
    };

    const incrementCount = () => {
      count.value++;
    };

    // Sample data for list rendering examples
    const myObject = { key1: 'ABCD', key2: 'EFGH' };
    const items = [
      { id: 1, name: 'ABCD' },
      { id: 2, name: 'EFGH' },
      { id: 3, name: 'IJKL' },
      { id: 4, name: 'MNOP' },
      { id: 5, name: 'QRST' },
    ];

    // Computed property for filteredItems
    const filteredItems = computed(() => {
      return items.filter(item => item.name.includes('A')); // Example condition
    });

    // Toggle Text
    const isTextVisible = ref(true);
    const toggleText = () => {
      isTextVisible.value = !isTextVisible.value;
    };

    return {
      message,
      rawHTML,
      inputId,
      count,
      inputValue,
      computedProperty,
      isActive,
      hasError,
      textColor,
      fontSize,
      textValue,
      trimmedTextValue,
      radioValue,
      selectedOption,
      numericValue,
      uppercaseMessage,
      handleClickInline,
      handleClickMethod,
      myObject,
      items,
      filteredItems,
      isTextVisible,
      toggleText,
    };
  },
};
</script>

<style scoped>
/* Container style */
.container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  /* Divide the container into two columns */
  gap: 20px;
  /* Add some spacing between output sections */
}

/* Style for even-indexed output sections */
.output:nth-child(even) {
  background-color: #f0f0f0;
  /* Apply background color to alternate sections */
}

/* Style for buttons */
button {
  background-color: #007bff;
  /* Blue background color */
  color: #fff;
  /* White text color */
  padding: 10px 20px;
  border: none;
  cursor: pointer;
}

/* Style for input and select elements */
input[type="text"],
input[type="number"],
textarea,
select {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

/* Style for radio button */
input[type="radio"] {
  margin-right: 5px;
}

/* Style for the "Toggle Text" button */
button#toggleTextButton {
  background-color: #28a745;
  /* Green background color */
}

/* Style for the message text */
p.message {
  font-size: 18px;
  font-weight: bold;
  color: #333;
}

/* Style for the raw HTML */
div.raw-html {
  margin-top: 10px;
  padding: 10px;
  background-color: #ffc107;
  /* Yellow background color */
}

/* Style for the list items */
ul li {
  list-style-type: square;
  font-weight: bold;
}

/* Style for the computed property text */
p.computed-property {
  font-style: italic;
}
</style>
