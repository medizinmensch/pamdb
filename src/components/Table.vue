<template>
  <!-- This example requires Tailwind CSS v2.0+ -->
  <div>
    <!-- <input type="text" class="w-100" /> -->
    <input
      type="text"
      name="search_string"
      id="search_string"
      v-model="this.search"
      class="focus:ring-indigo-500 focus:border-indigo-500 flex-1 block w-full rounded-r sm:text-sm border-gray-500 m-2 p-2"
      placeholder="Search for everything"
    />
  </div>
  <div class="flex flex-col">
    <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
        <div
          class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg"
        >
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-50">
              <tr>
                <th scope="col" class="py-3 px-0 font-medium text-gray-500">
                  Live
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Title
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Difficulty / Equipment
                </th>
                <th scope="col" class="relative px-6 py-3">
                  <span class="sr-only">Edit</span>
                </th>
              </tr>
            </thead>
            <tbody class="bg-white divide-y divide-gray-200">
              <tr v-for="item in filteredItems" :key="item.id">
                <td>
                  <div v-if="!item.live" class="w-4 h-20 bg-red-300"></div>
                </td>
                <td class="p-0 m-0 whitespace-nowrap">
                  <div class="flex items-center">
                    <div class="flex-shrink-2 w-36">
                      <a :href="item.link"> 
                      <img :src="item.image" alt=""/>

                      </a>
                      <!-- class="h-10 w-10 rounded-full" -->
                    </div>
                    <div class="ml-4">
                      <div class="text-sm font-medium text-gray-900">
                        {{ item.heading }}
                      </div>
                      <div class="text-sm text-gray-500">
                        {{ item.subtitle }}
                      </div>
                    </div>
                  </div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-sm text-gray-900">
                    {{ item.difficulty }}
                  </div>
                  <div
                    class="text-sm text-gray-500 rounded-full bg-green-100 text-green-800 inline-flex px-1.5"
                  >
                    {{ item.equipment }}
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Fuse from "fuse.js";

export default {
  computed: {
    filteredItems() {
      if (this.search == "") {
        return this.items;
      }

      const options = {
        includeScore: false,
        keys: this.propsToSearch,
      };

      const fuse = new Fuse(this.items, options);

      return fuse.search(this.search).map((e) => {
        return e.item;
      });
    },
  },
  data() {
    return {
      search: "",
      calories: "",
      propsToSearch: [
        "orig_title",
        "heading",
        "subtitle",
        "length",
        "titleLength",
        "accent_color",
        "workout_type",
        "tags",
        "difficulty",
        "trains",
        "scenery",
        "equipment",
        "together",
        "easter_eggs",
        "songs",
      ],
      items: [
        {
          id: 1,
          orig_title:
            "10 MIN FULL BODY STRETCH - a simple routine for tight muscles & flexibility I Pamela Reif",
          heading: "FULL BODY STRETCH",
          subtitle: "a simple routine for tight muscles & flexibility",
          length: "0:11:11",
          titleLength: 10,
          image: "/assets/images/xOqGI7EDe6U.jpg",
          accent_color: "#b2b0a9",
          workout_type: "stretching",
          tags: "",
          difficulty: "unknown",
          live: false,
          trains: "-",
          scenery: "harbour",
          equipment: "none",
          together: "none",
          easter_eggs: "none",
          songs: "tbd",
          link:
            "https://www.youtube.com/watch?v=xOqGI7EDe6U&list=PLEkRYDcpWohz_4X6qnkGeah-2lCVzHfg5",
        },
        {
          id: 2,
          orig_title:
            "30 MIN FULL BODY STRETCHING - perfect for rest days / No Equipment I Pamela Reif",
          heading: "FULL BODY STRETCHING",
          subtitle: "perfect for rest days / No Equipment",
          length: "0:31:17",
          titleLength: 30,
          image: "./assets/images/lJUIDBBqJOE.jpg",
          accent_color: "#fbe2c8",
          workout_type: "stretching",
          tags: "male-friendly",
          difficulty: "unknown",
          live: false,
          trains: "-",
          scenery: "home",
          equipment: "none",
          together: "none",
          easter_eggs: "none",
          songs: "tbd",
          link:
            "https://www.youtube.com/watch?v=lJUIDBBqJOE&list=PLEkRYDcpWohzRZv_90dWB6NF5-X7DfmGm",
        },
        {
          id: 3,
          orig_title:
            "10 MIN BEGINNER AB WORKOUT // No Equipment | Pamela Reif",
          heading: "BEGINNER AB WORKOUT",
          subtitle: "No Equipment",
          length: "0:10:29",
          titleLength: 10,
          image: "./assets/images/1f8yoFFdkcY.jpg",
          accent_color: "#e2a6cf",
          workout_type: "Classic workout",
          tags: "",
          difficulty: "Beginner Friendly",
          live: false,
          trains: "abs",
          scenery: "studio",
          equipment: "none",
          together: "none",
          easter_eggs: "none",
          songs: "tbd",
          link:
            "https://www.youtube.com/watch?v=1f8yoFFdkcY&list=PLEkRYDcpWohxNOnHpbAL6UOU1tfoOwUjv",
        },
        {
          id: 4,
          orig_title:
            "10 MIN AB WORKOUT - Back & Neck Friendly / No Equipment I Pamela Reif",
          heading: "AB WORKOUT",
          subtitle: "Back & Neck Friendly",
          length: "0:10:29",
          titleLength: 10,
          image: "./assets/images/l2AHpn2i7_Y.jpg",
          accent_color: "#c8e7eb",
          workout_type: "Classic workout",
          tags: "back & neck friendly",
          difficulty: "Medium Level",
          live: false,
          trains: "abs",
          scenery: "harbour",
          equipment: "none",
          together: "none",
          easter_eggs: "none",
          songs: "tbd",
          link:
            "https://www.youtube.com/watch?v=l2AHpn2i7_Y&list=PLEkRYDcpWohw0enIOyCm1x8jv5MDCqbFe",
        },
      ],
    };
  },
};
</script>