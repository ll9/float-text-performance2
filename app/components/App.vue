<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <StackLayout columns="*" rows="*">
            <WebView src="https://openlayers.org/en/latest/examples/cluster.html" style="height: 50%" />
            <Button text="nav" @tap="nav" />
        </StackLayout>
    </Page>
</template>

<script>
import SecondPage from './SecondPage';

  export default {
    data() {
      return {
        msg: 'Hello World!'
      }
    },
    methods: {
        nav() {
            this.$navigateTo(SecondPage, {transition: {name: 'slide', duration: 370}});
        }
    }
  }
</script>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }
</style>
