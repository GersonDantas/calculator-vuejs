<template>
  <div class="calculator">
    <Display :value="displayValue" />
    <ButtonCalculator label="AC" triple @onClick="clearMemory" />
    <ButtonCalculator label="/" @onClick="setOperation" operation />
    <ButtonCalculator label="7" @onClick="addDigit" />
    <ButtonCalculator label="8" @onClick="addDigit" />
    <ButtonCalculator label="9" @onClick="addDigit" />
    <ButtonCalculator label="*" @onClick="setOperation" operation />
    <ButtonCalculator label="4" @onClick="addDigit" />
    <ButtonCalculator label="5" @onClick="addDigit" />
    <ButtonCalculator label="6" @onClick="addDigit" />
    <ButtonCalculator label="+" @onClick="setOperation" operation />
    <ButtonCalculator label="1" @onClick="addDigit" />
    <ButtonCalculator label="2" @onClick="addDigit" />
    <ButtonCalculator label="3" @onClick="addDigit" />
    <ButtonCalculator label="-" @onClick="setOperation" operation />
    <ButtonCalculator label="0" @onClick="addDigit" double />
    <ButtonCalculator label="." @onClick="addDigit" />
    <ButtonCalculator label="=" @onClick="setOperation" operation />
  </div>
</template>

<script>
import Display from "@/components/Display"
import ButtonCalculator from "@/components/Button"

export default {
  data () {
    return {
      displayValue: "0",
      clearDisplay: false,
      operation: null,
      values: [0, 0],
      current: 0
    }
  },
  components: {
    Display,
    ButtonCalculator
  },
  methods: {
    clearMemory () {
      // console.log(this.$options.data())
      Object.assign(this.$data, this.$options.data())
    },
    setOperation (operation) {
      console.log(this.operation)
      if (this.current == 0) {
        this.operation = operation
        this.current = 1
        this.clearDisplay = true
      } else {
        const equals = operation === "="
        const currentOperation = this.operation

        try {
          this.values[0] = eval(
            `${this.values[0]} ${currentOperation} ${this.value[1]}`
          )
        } catch (error) {
          this.$emit('onError', error.message)
        }

        this.values[1] = 0

        this.displayValue = this.values[0]
        this.operation = equals ? null : operation
        this.current = equals ? 0 : 1
        this.clearDisplay = !equals
      }
    },
    addDigit (digit) {
      if (digit == "." && this.displayValue.includes(".")) {
        return
      }

      const clearDisplay = this.displayValue == "0" || this.clearDisplay
      console.log(clearDisplay, this.displayValue, this.clearDisplay)
      const currentValue = clearDisplay ? "" : this.displayValue
      const displayValue = currentValue + digit

      this.displayValue = displayValue
      this.clearDisplay = false
      this.values[this.current] = displayValue
    }
  },
}
</script>

<style>
.calculator {
  height: 320px;
  width: 235px;
  border-radius: 5px;
  overflow: hidden;

  display: grid;
  grid-template-columns: repeat(4, 25%);
  grid-template-rows: 1fr 48px 48px 48px 48px 48px;
}
</style>
