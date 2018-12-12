<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!"/>
    <ScrollView>
        <ListView for="item in arr">
          <v-template>
            <FloatText :keyboardType="item % 2 == 0 ? 'number': 'url'" :hint="item"/>
          </v-template>
        </ListView>
    </ScrollView>
  </Page>
</template>

<script>
import FloatText from "./sub/FloatText";

export default {
  data() {
    return {
      arr: Array.from(Array(40).keys()),
      msg: "Hello World!"
    };
  },
  components: {
    FloatText
  }
};
</script>

<style scoped>
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}

StackLayout {
  padding: 10;
  margin: 10;
  border-color: black;
  border-width: 3;
  border-radius: 5;
}

.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
</style>
