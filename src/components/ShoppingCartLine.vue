<template>
  <tr>
    <td>
      <input
        type="number"
        class="form-control-sm"
        style="width:5em"
        :value="qvalue"
        @input="sendChangeEvent"
      >
    </td>
    <td>{{ line.product.name }}</td>
    <td class="text-right">{{ line.product.price | currency }}</td>
    <td class="text-right">{{ (line.quantity * line.product.price) | currency }}</td>
    <td class="text-center">
      <button class="btn btn-sm btn-danger" @click="sendRemoveEvent">Remove</button>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    line: {
      type: Object,
      required: true
    }
  },
  data: function() {
    return {
      qvalue: this.line.quantity
    };
  },
  methods: {
    sendChangeEvent(e) {
      if (e.target.value > 0) {
        this.$emit("quantity", +e.target.value);
        this.qvalue = e.target.value;
      } else {
        this.$emit("quantity", 1);
        this.qvalue = 1;
        e.target.value = this.qvalue;
      }
    },
    sendRemoveEvent() {
      this.$emit("remove", this.line);
    }
  }
};
</script>