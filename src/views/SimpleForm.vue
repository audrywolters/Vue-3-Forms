<template>
  <div>
    <h1>Create an event</h1>
    <form @submit.prevent="sendForm">

      <BaseSelect 
        :options="categories"
        v-model="event.category"
        label="Select a Category"
      />

      <h3>Name & describe your event</h3>

      <BaseInput
        v-model="event.title"
        label="Title"
        type="text"
      />

      <BaseInput
        v-model="event.description"
        label="Description"
        type="text"
      />

      <h3>Where is your event?</h3>

      <BaseInput
        v-model="event.location"
        label="Location"
        type="text"
      />

      <h3>Are pets allowed?</h3>
      <div>
        <BaseRadioGroup
          v-model="event.pets"
          name="pets"
          :options="petOptions"
        />
      </div>

      <h3>Extras</h3>
      <div>
        <BaseCheckbox
          v-model="event.extras.catering"
          label="Catering"
        />
      </div>

      <div>
        <BaseCheckbox
          v-model="event.extras.music"
          label="Live Music"
        />
      </div>

      <button class="button -fill-gradient" type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
import BaseInput from "../components/BaseInput.vue"
import BaseSelect from "../components/BaseSelect.vue";
import BaseCheckbox from "../components/BaseCheckbox.vue";
import BaseRadio from "../components/BaseRadio.vue";
import BaseRadioGroup from "../components/BaseRadioGroup.vue";
export default {
    data() {
        return {
            categories: [
                "sustainability",
                "nature",
                "animal welfare",
                "housing",
                "education",
                "food",
                "community"
            ],
            event: {
                category: "",
                title: "",
                description: "",
                location: "",
                pets: 1,
                extras: {
                    catering: false,
                    music: false
                }
            },
            petOptions: [
              { label: 'Yes', value: 1 },
              { label: 'No', value: 0 }
            ]
        };
    },
    methods: {
      sendForm() {
        axios.post(
          'https://my-json-server.typicode.com/Code-Pop/Vue-3-Forms/events',
          this.event
        )
        .then(function (response) {
          console.log('Repsonse: ', response)
        })
        .catch(function (err) {
          console.log('Error: ', err)
        })
      }
    },
    components: { BaseInput, BaseSelect, BaseCheckbox, BaseRadio, BaseRadioGroup }
}
</script>
