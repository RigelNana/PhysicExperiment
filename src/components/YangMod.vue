<!--<script>-->
<!--export default {-->
<!--  data() {-->
<!--    return {-->
<!--      headers: ['value1', 'value2',"value3"],-->
<!--      rows: [-->
<!--        { values: [10, 20, 30] },-->
<!--        { values: [40, 50, 60] },-->
<!--        { values: [70, 80, 90] },-->
<!--      ]-->
<!--    };-->
<!--  }-->
<!--};-->
<!--</script>-->

<!--<template>-->
<!--  <div>-->
<!--    <table>-->
<!--      <thead>-->
<!--      <tr>-->
<!--        <th v-for="header in headers" :key="header">{{ header }}</th>-->
<!--      </tr>-->
<!--      </thead>-->
<!--      <tbody>-->
<!--      <tr v-for="(row, index) in rows" :key="index">-->
<!--        <td v-for="(value,idx) in row.values" :key="idx">-->

<!--          <input type="number" v-model.number="value" />-->
<!--        </td>-->
<!--      </tr>-->
<!--      </tbody>-->
<!--    </table>-->
<!--  </div>-->
<!--</template>-->

<!--<style scoped>-->

<!--</style>-->
<!--<template>-->
<!--  <table>-->
<!--    <thead>-->
<!--    <tr>-->
<!--      <th v-for="header in headers" :key="header">{{ header }}</th>-->
<!--      <th>Average</th>-->
<!--    </tr>-->
<!--    </thead>-->
<!--    <tbody>-->
<!--    <tr v-for="(row, rowIndex) in rows" :key="rowIndex">-->
<!--      <td v-for="(value, valueIndex) in row.values" :key="valueIndex">-->
<!--        <input type="number"-->
<!--               :value="value"-->
<!--               @input="handleInput($event, rowIndex, valueIndex)" />-->
<!--      </td>-->
<!--      <td>{{ calculateAverage(row.values) }}</td>-->
<!--    </tr>-->
<!--    </tbody>-->
<!--  </table>-->
<!--</template>-->

<!--<script>-->
<!--export default {-->
<!--  data() {-->
<!--    return {-->
<!--      headers: ['Value 1', 'Value 2', 'Value 3'],-->
<!--      rows: [-->
<!--        { values: [10, 20, 30] },-->
<!--        { values: [40, 50, 60] },-->
<!--        { values: [70, 80, 90] },-->
<!--      ],-->
<!--    };-->
<!--  },-->
<!--  methods: {-->
<!--    handleInput(event, rowIndex, valueIndex) {-->
<!--      this.rows[rowIndex].values[valueIndex] = Number(event.target.value); // 更新指定位置的值-->
<!--    },-->
<!--    calculateAverage(values) {-->
<!--      const total = values.reduce((acc, cur) => acc + cur, 0);-->
<!--      return (total / values.length).toFixed(2);-->
<!--    }-->
<!--  }-->
<!--};-->
<!--</script>-->
<template>
  <div>
    <h1>实验数据测量</h1>

    <!-- 一次性测量 -->
    <h2>1. 一次性测量</h2>
    <table>
      <tr>
        <th>描述</th>
        <th>测量值 (mm)</th>
        <th>误差 (mm)</th>
      </tr>
      <tr>
        <td>金属丝原长 L</td>
        <td><input type="number" v-model="length" > </td>
        <td>±2</td>
      </tr>
      <tr>
        <td>垂直距离 H</td>
        <td>{{ measurements.height }}</td>
        <td>±2</td>
      </tr>
    </table>

    <!-- 金属丝直径测量 -->
    <h2>2. 金属丝直径测量</h2>
    <div>
      <p>零差d0 (mm): 0.004</p>
      <p>Δ0 (mm): 0.004</p>
    </div>
    <table>
      <tr>
        <th>次数</th>
        <th v-for="n in 6">{{ n }}</th>
      </tr>
      <tr>
        <td>直径 d (mm)</td>
        <td v-for="(d, index) in diameters" :key="index">
          <input type="number" v-model="diameters[index]" />
        </td>
      </tr>
    </table>
    <div>
      <p>平均值: {{ this.average(diameters) }}</p>
      <p>标准差: {{ this.stdDeviation(diameters) }}</p>
      <p>Δd (mm): 0.005</p>
    </div>

    <!-- 支点到动足距离测量 -->
    <h2>3. 支点到动足距离测量</h2>
    <div>
      <p>Δ0 (mm): 0.02</p>
    </div>
    <table>
      <tr>
        <th>次数</th>
        <th v-for="n in 6">{{ n }}</th>
      </tr>
      <tr>
        <td>长度 b (mm)</td>
        <td v-for="(b, index) in lengths" :key="index">
          <input type="number" v-model="lengths[index]" />
        </td>
      </tr>
    </table>
    <div>
      <p>平均值: {{ this.average(diameters) }}</p>
      <p>标准差: {{ this.stdDeviation(diameters) }}</p>
      <p>Δd (mm): 0.005</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      measurements: {
        length: 0,
        height: 0
      },
      diameters: Array(6).fill(null),
      lengths: Array(6).fill(null)
    };
  },

  methods:{
    average(data) {
      const sum = data.reduce((acc, val) => acc + (val || 0), 0);
      return (sum / data.length);
    },
    stdDeviation(data) {
      const mean = this.average(data);
      const variance = data.reduce((acc, val) => {
        return acc + ((val || 0) - mean) ** 2;
      }, 0) / (data.length - 1);
      return Math.sqrt(variance);
    }
  }
};
</script>
<style>

</style>