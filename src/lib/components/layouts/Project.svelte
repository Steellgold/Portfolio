<script lang="ts">
  import Button from "$lib/components/elements/navigation/Button.svelte";
  import ButtonGroup from "../elements/containers/ButtonGroup.svelte";

  interface YearProp {
    from: string;
    to?: string;
    paused?: boolean;
  }

  interface ButtonProp {
    text: string;
    link: string;
    icon: string;
  }
  
  export let title: string;
  export let year: YearProp;
  export let smallDescription: string | undefined = undefined;

  export let primaryTechIcon: string;
  export let techIcons: string[];
  
  export let button: ButtonProp | undefined = undefined;
  export let buttons: ButtonProp[] | undefined = undefined;
</script>

<div class="card">
  <!-- Primary language used -->
  <div class="lang">
    <img src={primaryTechIcon} alt="primary skill"/>
  </div>

  <!-- Title and dates -->
  <div class="title-date">
    <h2>{title}</h2>

    {#if year.paused}
      <p>Paused</p>
    {:else}
      {#if year.from !== "0"}
        <p>{`${year.from} → ${year.to ? year.to : "now"}`}</p>
      {/if}
    {/if}
  </div>

  <!-- Description -->
  <div class="description">
    <a href={`/project/${title}`} class="toPage">
      <p>{@html smallDescription}</p>
    </a>
  </div>

  <!-- Technos -->
  <div class="skills">
    <p>Technologies used:</p>

    <div>
      {#each techIcons as tech}
        <img src={tech} alt="a used tech">
      {/each}      
    </div>
  </div>

  <!-- Button -->
  {#if button}
    <Button link={button.link} icon={button.icon} small={true}>{button.text}</Button>
  {/if}

  {#if buttons !== undefined}
    <ButtonGroup>
      {#each buttons as button}
        <Button link={button.link} icon={button.icon} small={false}>{button.text}</Button>
      {/each}
    </ButtonGroup>
  {/if}
</div>

<style lang="scss">
  @import "../../scss/variables.scss";

  .card {
    a.toPage {
      color: white;
      text-decoration: none;
    }

    position: relative;

    background: $color-background;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 15px;
    
    height: 400px;
    margin-top: 30px; // for fix the techno absolute element size
    padding: 30px 15px;
    
    border: 8px solid #FFFFFF;
    border-radius: 30px;
    
    text-align: center;

    .lang {
      position: absolute;
      top: -35px;
      left: 50%;
      transform: translateX(-50%);

      width: 50px;
      height: 50px;
      
      background-color: white;

      border: 5px solid white;
      border-radius: 10px;

      img {
        height: 100%;
        width: 100%;
      }
    }

    .title-date {
      margin-top: 10px;

      display: grid;
      place-content: center;
    }

    .description {
      height: 200px;
    }

    .skills {
      display: flex;
      flex-direction: column;
      gap: 5px;

      p {
        font-weight: bold;
      }

      div {
        display: flex;
        justify-content: center;
        gap: 5px;

        img {
          height: 40px;
          width: auto;
          border-radius: 10px;
        }
      }
    }
  }
</style>