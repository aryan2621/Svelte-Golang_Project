<script lang="ts">
  import { onMount } from "svelte";
  import { EXERCISE_API_DETAILS } from "../API/api";
  import axios from "axios";

  let exersiseForAllBodyParts: any = [];

  onMount(async () => {
    let options = {
      url: EXERCISE_API_DETAILS.BASE_URL,
      headers: {
        "X-Api-Key": EXERCISE_API_DETAILS.HEADERS.KEY,
      },
    };
    axios
      .request(options)
      .then(function (response) {
        console.log(response.data);
        exersiseForAllBodyParts = response.data.splice(0, 6);
        exersiseForAllBodyParts.forEach(async (exercise: any) => {
          const imageURL = await returnImageFromURL(exercise.muscle);
          exercise.imageURL = imageURL;
        });
      })
      .catch(function (error) {
        console.error(error);
      });
  });
  const truncate = (str: string, isTruncated: boolean) => {
    if (isTruncated) {
      return str.substring(0, 100);
    } else {
      return str;
    }
  };

  export const returnImageFromURL = async (query: string) => {
    let api = "6wuULxAn64ad6su9YkkFgAj8dbo0AfJNzeRGP77OC3MCJ3otjDFYFlSa";
    const URL = `https://api.pexels.com/v1/search?query=${query}&per_page=1&page=1`;
    const response = await fetch(URL, {
      headers: {
        Authorization: api,
      },
    });
    const data = await response.json();
    console.log(data)
    const imageURL = data.photos[0].src.original;
    return imageURL;
  };
  
</script>

<main>
  <div class="container my-24 px-6 mx-auto">
    <section class="mb-32 text-gray-800 text-center">
      <h2 class="text-3xl font-bold mb-12">Testimonials</h2>
      <div class="grid md:grid-cols-3 gap-x-6 lg:gap-x-12">
        {#each exersiseForAllBodyParts as exercise}
          <div class="mb-12 md:mb-0">
            <div class="flex justify-center mb-6">
              <img src={exercise.imageURL}  class="rounded-full shadow-lg w-32" alt="" />
            </div>
            <h5 class="text-lg font-bold mb-4">{exercise.name}</h5>
            <h6 class="font-medium text-blue-600 mb-4">
              {exercise.difficulty}
            </h6>
            <p class="mb-4">
              <svg
                aria-hidden="true"
                focusable="false"
                data-prefix="fas"
                data-icon="quote-left"
                class="w-6 pr-2 inline-block"
                role="img"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 512 512"
              >
                <path
                  fill="currentColor"
                  d="M464 256h-80v-64c0-35.3 28.7-64 64-64h8c13.3 0 24-10.7 24-24V56c0-13.3-10.7-24-24-24h-8c-88.4 0-160 71.6-160 160v240c0 26.5 21.5 48 48 48h128c26.5 0 48-21.5 48-48V304c0-26.5-21.5-48-48-48zm-288 0H96v-64c0-35.3 28.7-64 64-64h8c13.3 0 24-10.7 24-24V56c0-13.3-10.7-24-24-24h-8C71.6 32 0 103.6 0 192v240c0 26.5 21.5 48 48 48h128c26.5 0 48-21.5 48-48V304c0-26.5-21.5-48-48-48z"
                />
              </svg>
              {truncate(exercise.instructions, true)}...
            </p>
          </div>
        {/each}
      </div>
    </section>
  </div>
</main>
