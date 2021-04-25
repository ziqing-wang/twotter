<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1>{{ user_profile["username"] }}</h1>
      <div class="user-profile_admin-badge" v-if="user_profile['isAdmin']">
        admin
      </div>
      <p><strong>Followers: </strong>{{ user_profile["followers"] }}</p>

      <form
        class="user-profile_create-twoot"
        :class="{ exceeded: newTwootContent.length > maxCharacters }"
        @submit.prevent="addNewTwoot"
      >
        <label for="newTwoot" class="label-for-new-twoot"
          ><strong>New Twoot </strong>
          <span>({{ countCharacters }} / {{ maxCharacters }})</span>
        </label>
        <textarea
          name="New Twoot"
          id="newTwoot"
          :cols="textCols"
          :rows="textRows"
          v-model="newTwootContent"
        ></textarea>

        <div class="user-profile_new-twoot-type">
          <label for="newTwootType">Type: </label>
          <select
            name="New Twoot Type"
            id="newTwootType"
            v-model="selectedType"
          >
            <option
              v-for="(option, index) in new_twoot_types"
              :value="option['value']"
              :key="index"
              >{{ option["name"] }}</option
            >
          </select>
        </div>

        <button type="submit" class="new-twoot-btn">Twoot</button>
      </form>
    </div>

    <div class="user-profile__twoot-wrapper">
      <twoot-item
        v-bind:twootDate="twoot['date']"
        v-for="(twoot, index) in twoots"
        :key="index"
        v-bind:twoot="twoot"
      ></twoot-item>
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem.vue";

export default {
  name: "UserProfile",
  components: {
    TwootItem
  },
  data() {
    return {
      user_profile: {
        username: "@Roronoa_zoro",
        firstname: "Zoro",
        lastname: "Roronoa",
        followers: 0,
        isAdmin: true
      },
      newTwootContent: "",
      selectedType: "instant twoot",
      twootDate: "",
      new_twoot_types: [
        {
          id: 1,
          value: "draft",
          name: "Draft"
        },
        {
          id: 2,
          value: "instant twoot",
          name: "Instant Twoot"
        }
      ],

      twoots: [
        {
          id: 1,
          date: "15 Apr, 2021",
          content: "This is a simple twotter demo created on Vue."
        },
        {
          id: 2,
          date: "25 Feb, 2021",
          content: "Hello world."
        }
      ],
      maxCharacters: 100,
      textCols: 10,
      textRows: 10
    };
  },

  computed: {
    //count the characters user typed in
    countCharacters() {
      return this.newTwootContent.length;
    }
  },
  methods: {
    //get the current date
    getCurrentDate() {
      const date = new Date();
      const year = date.getFullYear();
      const monthNumber = date.getMonth();
      const day = date.getUTCDate();

      const months = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "June",
        "July",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec"
      ];
      const month = months[monthNumber];
      const currentDate = `${day} ${month}, ${year}`;
      return currentDate;
    },
    //add new twoot
    addNewTwoot() {
      if (this.newTwootContent !== "" && this.selectedType !== "draft") {
        let len = this.twoots.length;
        const currentDate = this.getCurrentDate();
        this.twoots.unshift({
          id: len + 1,
          date: currentDate,
          content: this.newTwootContent
        });

        //clear the textarea
        this.newTwootContent = "";
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;
  text-align: left;

  /* user basic profile */
  .user-profile_user-panel {
    display: flex;
    flex-direction: column;
    background-color: #fff;
    padding: 20px;
    border-radius: 5px;
    border: 1px solid #dfe3e8;

    /* login as admin */
    .user-profile_admin-badge {
      background-color: rebeccapurple;
      color: #fff;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
  }

  /* stypes for create new twoot */
  .user-profile_create-twoot {
    padding-top: 20px;
    display: flex;
    flex-direction: column;

    #newTwoot,
    .new-twoot-btn {
      margin: 10px 0;
    }
    #newTwoot {
      border-color: #dfe3e8;
    }
    .new-twoot-btn {
      background-color: rebeccapurple;
      color: #fff;
      padding: 10px 12px;
      border-radius: 5px;
      outline: none;
      border: none;
      cursor: pointer;
    }
  }
  /* invalid input: out the limit of characters or the input is empty*/
  .exceeded {
    .label-for-new-twoot {
      color: red;
    }
    #newTwoot {
      outline: none;
      border-color: red;
    }
    .new-twoot-btn {
      background-color: gray;
      pointer-events: none;
    }
  }
}

@media (max-width: 768px) {
  .user-profile {
    grid-template-columns: 1fr; /* repeat(auto-fill, minmax(350px, 1fr)) */
    padding: 20px;
  }
}
</style>
