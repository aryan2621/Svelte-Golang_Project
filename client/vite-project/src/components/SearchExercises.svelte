<script lang="ts">
  import { EXERCISE_API_DETAILS } from "../API/api";
  import axios from "axios";

  let exercise: string = "";
  export let exerciseData: any = [];
  let sumitted: boolean = false;

  const handleSubmit = async () => {
    if (exercise.length > 0) {
      let options = {
        url: EXERCISE_API_DETAILS.BASE_URL + exercise,
        headers: {
          "X-Api-Key": EXERCISE_API_DETAILS.HEADERS.KEY,
        },
      };
      console.log(options);
      axios
        .request(options)
        .then(function (response) {
          console.log(response.data);
          exerciseData = response.data;
          sumitted = true;
        })
        .catch(function (error) {
          console.error(error);
        });
    }
  };
</script>

<main>
  <div
    data-aos="fade-right"
    class="flex justify-center my-5 text-center"
  >
    <div class="mb-3 w-4/5">
      <form on:submit|preventDefault={handleSubmit}>
        <label
          for=""
          class=" mt-5 text-3xl font-bold tracking-tight text-white-900 sm:text-4xl m-auto"
          >Awesome Exercises You Should Know.</label
        >
        <input
          type="text"
          class="
                    form-control
                    px-3
                    py-1.5
                    text-base
                    font-normal
                    text-white-700
                    bg-white bg-clip-padding
                    border border-solid border-gray-300
                    rounded
                    transition
                    ease-in-out
                    mt-5
                    w-4/5
                    focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none
                  "
          placeholder="Search for exercises"
          bind:value={exercise}
        />
        <button
          type="submit"
          class="bg-transparent hover:bg-blue-500 text-white-700 font-semibold hover:text-white py-1 px-4 border border-blue-500 hover:border-transparent rounded"
        >
          Button
        </button>
      </form>
    </div>
  </div>
  <div class="mb-3 w-full" data-aos="fade-left">
    {#if exerciseData && exerciseData.length > 0}
      <div class="flex justify-center">
        <div
          class="flex flex-col md:flex-row md:max-w-xl rounded-lg bg-white shadow-lg"
        >
          <img
            class=" w-full h-96 md:h-auto object-cover md:w-48 rounded-t-lg md:rounded-none md:rounded-l-lg"
            src="https://mdbootstrap.com/wp-content/uploads/2020/06/vertical.jpg"
            alt=""
          />
          <div class="p-6 flex flex-col justify-start">
            <h5 class="text-gray-900 text-xl font-medium mb-2">
              {exerciseData[0].name}
            </h5>
            <p class="text-gray-700 text-base mb-4">
              {exerciseData[0].instructions}
            </p>
            <p class="text-gray-600 text-xs">{exerciseData[0].difficulty}</p>
          </div>
        </div>
      </div>
    {:else if exerciseData.length === 0 && exercise.length > 0 && sumitted}
      <div
        class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative"
        role="alert"
      >
        <strong class="font-bold">Holy smokes!</strong>
        <span class="block sm:inline">Something seriously bad happened.</span>
        <span class="absolute top-0 bottom-0 right-0 px-4 py-3">
          <svg
            class="fill-current h-6 w-6 text-red-500"
            role="button"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
            ><title>Close</title><path
              d="M14.348 14.849a1.2 1.2 0 0 1-1.697 0L10 11.819l-2.651 3.029a1.2 1.2 0 1 1-1.697-1.697l2.758-3.15-2.759-3.152a1.2 1.2 0 1 1 1.697-1.697L10 8.183l2.651-3.031a1.2 1.2 0 1 1 1.697 1.697l-2.758 3.152 2.758 3.15a1.2 1.2 0 0 1 0 1.698z"
            /></svg
          >
        </span>
      </div>
    {/if}
  </div>
</main>
