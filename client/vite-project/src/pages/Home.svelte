<script lang="ts">
  import Exercises from "../components/Exercises.svelte";
  import HeroBanner from "../components/HeroBanner.svelte";
  import SearchExercises from "../components/SearchExercises.svelte";

  let bodyPart: string = "";
  let exercises: any = [];
</script>

<main>
  <HeroBanner />
  <SearchExercises bodypart={bodyPart} {setExercises} {setBodyPart} />
  <Exercises bodypart={bodyPart} {setExercises} {setBodyPart} />
</main>
