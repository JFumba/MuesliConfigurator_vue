<template>
    <div class="container">
        <MealConfiguratorProgress 
        :activeConfigStep="activConfigStep"
        :configuration="configuration"/>
        <div class="config-container">
            <div class="order-info">
                <dir>
                    <h1>Good Morning!</h1>
                    <h2>Choose the ingredients for your breakfast</h2>
                </dir>
            </div>
            <div class="selection">
                <h3>{{ configuration[activConfigStep].title }}</h3>
                <MealConfiguratorOptions 
                 v-if="activConfigStep +1 < configuration.length"
                 :activeConfigStep="activConfigStep"
                 :configuration="configuration"
                 @chooseOption="selectOption"/>
                 <MealConfiguratorOrder 
                 v-else
                 :configuration="configuration" />
            </div>
        </div>
    </div>
</template>

<script>
    import MealConfiguratorProgress from './MealConfiguratorProgress.vue'
    import MealConfiguratorOptions from './MealConfiguratorOptions.vue'
    import MealConfiguratorOrder from './MealConfiguratorOrder.vue'

export default {
    data: () => {
      return {
        activConfigStep: 0,
        configuration: [
          {
            title: 'Cereal base',
            selectedOption: {},
            options: [
              { title: 'Pure Oat Flakes', img: 'wheat.png', price: 2.99 },
              { title: 'Protein Flakes', img: 'wheat.png', price: 3.49 },
              { title: 'Crunchy Coffee', img: 'wheat.png', price: 3.49 },
              { title: 'Crunchy and Oat', img: 'wheat.png', price: 3.99 }
            ]
          },
          {
            title: 'Fruit',
            selectedOption: {},
            options: [
              { title: 'Apple', img: 'apple.png', price: 0.99 },
              { title: 'Fig', img: 'fig.png', price: 1.49 },
              { title: 'Apricot', img: 'apricot.png', price: 1.49 },
              { title: 'Plum', img: 'plum.png', price: 1.29 },
              { title: 'Strawberry', img: 'strawberry.png', price: 1.99 },
              { title: 'Raspberry', img: 'raspberry.png', price: 1.99 },
              { title: 'Banana', img: 'banana.png', price: 0.99 },
              { title: 'Blueberry', img: 'blueberry.png', price: 1.79 }
            ]
          },
          {
            title: 'Nuts and Seeds',
            selectedOption: {},
            options: [
              { title: 'Sunflower Seeds', img: 'sunflower.png', price: 0.49 },
              { title: 'Pumpkin Seeds', img: 'pumpkin-seed.png', price: 0.49 },
              { title: 'Hazelnuts', img: 'hazelnut.png', price: 0.99 },
              { title: 'Walnuts', img: 'nut.png', price: 1.29 },
              { title: 'Cashew Nuts', img: 'cashew.png', price: 0.99 },
              { title: 'Coconut Flakes', img: 'coconut.png', price: 1.49 },
              { title: 'Pecan Nuts', img: 'pecan.png', price: 0.99 }
            ]
          },
          {
            title: 'Chocolate',
            selectedOption: {},
            options: [
              { title: 'Dark Chocolate', img: 'chocolate.png', price: 1.49 },
              { title: 'White Chocolate', img: 'white-chocolate.png', price: 1.49 },
              { title: 'Espresso Chocs', img: 'espresso.png', price: 1.99 },
              { title: 'Chocolate Puffs', img: 'choco-puff.png', price: 1.49 }
            ]
          },
          {
            title: 'Bon appetite!',
            selectedOption: { title: 'Total', price: 0 },
          }
        ]
      }
    },
    components: {
        MealConfiguratorProgress,
        MealConfiguratorOptions,
        MealConfiguratorOrder
    },
    methods: {
      selectOption(option) {
        this.configuration[this.activConfigStep].selectedOption = option;
        this.activConfigStep += 1;

        if(this.activConfigStep + 1 === this.configuration.length) {
          let totalPrice = 0;
          this.configuration.forEach(element => {
            totalPrice += element.selectedOption.price;
          });

          this.configuration[this.activConfigStep]
            .selectedOption.price = totalPrice.toFixed(2);
        }
      }
    }
}
</script>

<style lang="scss" scoped>
  @import url('https://fonts.googleapis.com/css?family=Ubuntu&display=swap');
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 10px;
    width: calc(100% - 20px);
    min-height: calc(100vh - 20px);
    font-family: 'Ubuntu', Arial;
    font-size: 1rem;
    color: #333;
    background: url(../assets/app_breakfast.jpg) center center;
    background-size: cover;
    overflow: hidden;
  }
  .config-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
    width: 100%;
    max-width: 720px;
    min-height: 480px;
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 15px 30px rgba(0,0,0,.2),
                0 10px 10px rgba(0,0,0,.2);
  }
  .selection {
    min-height: 480px;
    background-color: rgba($color: #fff, $alpha: .8);
    overflow: hidden;
    h3 {
      text-align: center;
    }
  }
  .order-info {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    min-height: 480px;
    padding: 10px;
    color: #ddd;
    text-align: center;
    background-color: rgba($color: #28a1ba, $alpha: .8);
    @media only screen and (max-width: 740px) {
      min-height: fit-content;
    }
  }
</style>