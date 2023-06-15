<script lang="ts">
  /**
   * @type {{ title: string, description: string }}
   */
  // Declare a variable named "game" with the specified type
  export let game;
</script>

<!-- Card component -->
<div class="card">
  <!-- Image wrapper -->
  <div class="image-wrapper" />

  <!-- Play wrapper -->
  <div class="play-wrapper">
    <img src="/vector.png" alt="wrapper"/>
  </div>

  <!-- Play button -->
  <div class="play-button">
    <img src="/play.svg" alt="play"/>
  </div>

  <!-- Data section -->
  <section class="data">
    <!-- Game title -->
    <span class="data-title">{game.title}</span>

    <!-- Game description -->
    <p class="data-description">{game.description}</p>
  </section>
</div>


<style lang="scss">
  .card {
    width: 304px;
    height: 270px;
    background: #ffffff;
    border: 1px solid #dee1e4;
    border-radius: 15px;
    position: relative;
    overflow: hidden;

    .image-wrapper {
      height: 180px;
      background: #f4f5f6;
    }
    .play-wrapper {
      position: absolute;
      width: 84px;
      height: 30px;
      left: calc(50% - 84px/2);
      top: 150px;
    }
    .play-button {
      position: absolute;
      width: 40px;
      height: 40px;
      left: calc(50% - 40px / 2);
      top: 160px;

      background: linear-gradient(97.13deg, #0f853d 5.56%, #07652c 95.83%);
      border-radius: 20px;
    }
    .data {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: 26px;
      font-family: 'Lato';
       font-style: normal;
      &-title {
        font-weight: 500;
        font-size: 14px;
        line-height: 20px;
        color: #323232;
      }
      &-description {
        margin-top: 4px;
        font-weight: 400;
        font-size: 12px;
        line-height: 18px;
        color: #808080;
      }
    }
  }
</style>
