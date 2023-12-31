<template>
  <div id="kiwi">
    <h1>Endangered Birds of NZ</h1>
    <div class="top-left">
      <!-- Displaying formatted current date -->
      <p class="date">Today's Date: {{ formattedDate }}</p>

      <!-- Displaying custom formatted date -->
      <p class="date">Today's Day: {{ customFormattedDate }}</p>
    </div>
    <div class="center-content">
      <div class="fact-container">
        <h1 :style="{ color: headerColor }">Kakapo (Strigops habroptila)</h1>
        <p><b>The kakapo is the only flightless parrot in the world.</b></p>
      </div>
    </div>
    <br>
    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>Fact Type</th>
          <th>Details</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(fact, index) in facts" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ fact.type }}</td>
          <td>{{ fact.details }}</td>
        </tr>
      </tbody>
    </table>
    <br>
    <div class="image1">
      <img :src="kakapoImageUrl" alt="Kakapo Image" class="center">
      <p class="image-caption">(Image: <i>Department of Conservation, New Zealand)</i></p>
    </div>
    <br>
    <h2><i>Contact The Conservation</i></h2>
    <form @submit.prevent="validateForm">
      <label for="name">Name:</label>
      <input type="text" id="name" name="name" v-model="formData.name" required>
      <span class="error">{{ formErrors.name }}</span>
      <br><br>

      <label for="email">Email:</label>
      <input type="email" id="email" name="email" v-model="formData.email" required>
      <span class="error">{{ formErrors.email }}</span>
      <br><br>

      <label for="message">Message:</label>
      <textarea id="message" name="message" v-model="formData.message" required></textarea>
      <span class="error">{{ formErrors.message }}</span>
      <br><br>

      <input type="submit" value="Submit">
    </form>
    <div>
      <h2>Sirocco the Kakapo</h2>

      <div class="center">
        <iframe width="560" height="315" :src="kakapoVideoUrl" frameborder="0" allowfullscreen></iframe>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment';
export default {
  data() {
    return {
      headerColor: 'rgb(134, 198, 37)',
      currentDate: moment().toISOString(),
      populationCount: 247, // Replace with the actual live population count
      facts: [
        {
          type: "Habitat",
          details: "Kakapos are native to New Zealand and are mostly found in forested areas."
        },
        {
          type: "Population",
          details: "As of 2021, there are only around 200 kakapos left in the world."
        },
        {
          type: "Behaviour",
          details: "Kakapos are nocturnal, solitary birds known for their unique booming calls."
        }
      ],
      kakapoImageUrl: "https://www.doc.govt.nz/thumbs/hero/contentassets/22c4c0407c1142ffbd70ef6ff029d722/stella-the-kakapo-codfish-1600.jpg",
      kakapoVideoUrl: "https://www.youtube.com/embed/9T1vfsHYiKY",
      formData: {
        name: '',
        email: '',
        message: ''
      },
      formErrors: {
        name: '',
        email: '',
        message: ''
      },
      uppercaseResult: '',
      substringResult: ''
    };
  },
  computed: {
    // Format the current date
    formattedDate() {
      return moment(this.currentDate).format('MMMM Do YYYY, h:mm:ss a');
    },
    // Custom formatted date example
    customFormattedDate() {
      return moment(this.currentDate).format('dddd');
    }
  },
  methods: {
    validateForm() {
      // Validation logic here, similar to your validateForm function
      // Set formErrors appropriately
      // Return isValid

      // Example of updating data properties:
      this.uppercaseResult = "Title: " + this.formData.name.toUpperCase();
      this.substringResult = "Name: " + this.formData.name.substring(0, 7);
    },
    mounted() {
    // Code to set currentFullDate and currentTime properties
    const now = new Date();
    this.currentFullDate = "Full Date: " + now.toDateString();
    this.currentTime = "Time: " + now.toTimeString();
    
    // Update the population count
    this.updatePopulationCount();
    
    // Call the updatePopulationCount function every 1 minute (60000 milliseconds)
    setInterval(this.updatePopulationCount, 60000);
    },
    methods: {
      },
      updatePopulationCount() {
      // Replace this with code to fetch the actual live population count
      // For now, we'll just use the initial value for demonstration
      this.populationCount = 247;
    },
  },
};
</script>

<style scoped>
table {
  border-collapse: collapse;
  width: 100%;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

/* Style the table header */
th {
  background-color: #f2f2f2;
}

.header-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 20px;
  border-bottom: 1px solid #ddd;
}

.image1 img {
  max-width: 50%;
  height: auto;
}

.center {
  text-align: center;
}

.top-left {
  position: absolute;
  top: 0;
  left: 0;
  background-color: lightblue;
  padding: 10px;
  border-bottom-right-radius: 10px;
}

.date {
  margin: 0;
  font-size: 14px;
}

.fact-container {
  text-align: center;
}
</style>

<style>
.video-container iframe {
  width: 100%;
  max-height: 30%;
}
.center-image {
  display: block;
  margin: 0 auto;
}
.form-group {
  margin-bottom: 20px;
}
body {
    text-align: center;
    font-family: 'Times New Roman', Times, serif;
    line-height: 1.5;
    padding: 20px;
    background-color: lightblue;
  }
.contact-form {
  text-align: left;
}
.header-text {
  margin: 0;
}
.contact-title {
  color: #777;
  margin: 0;
}
.fact-card {
  border: 1px solid #ddd;
  padding: 10px;
  margin: 10px 0;
  background-color: #f9f9f9;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}
</style>
