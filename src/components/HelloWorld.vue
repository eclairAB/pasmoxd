<template>
  <v-container fluid>
    {{ messages }}

    <v-text-field v-model="msg" />
    <v-btn @click="send()">SEND</v-btn>
  </v-container>
</template>

<script>
  /* eslint-disable */
  import axios from 'axios'

  export default {
    data: () => ({
      messages: null,
      msg: ''
    }),
    sockets: {
        connect () {
          console.log('were fuckin connected')
        }
        /* channel_name (payload) {
            console.log(data)
        }*/
    },
    methods: {
      /* send () {
        axios.post('http://192.168.0.199:8000/api/post', {message: this.msg}).then(data => {
          console.log(data)
          this.$socket.client.emit("channel_name", data);
        }).catch(data => {
          console.log(data)
        })
      },
      subs () {
        this.$socket.$subscribe('Pasmo', payload => {
          console.log(payload)
        });
      }, */
      manual () {
        axios.get('http://192.168.0.199:8000/api/getAll').then(({data}) => {
          this.messages = data;
        });
      }
    },
    mounted () {
     // this.subs()
    },
    created() {
      this.manual()
    }
  }
</script>
