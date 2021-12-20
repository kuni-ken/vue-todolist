<template>
  <v-dialog
    v-model="show"
    max-width="600px"
    v-on:click:outside="cancel"
  >
    <v-card>
      <v-card-title>
        <span class="text-h5">ToDo</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col
              cols="12"
              sm="12"
              md="12"
            >
              <v-text-field
                label="タイトル*"
                required
                v-model="title"
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col
              cols="12"
              sm="12"
              md="12"
            >
              <v-textarea
                required
                label="詳細*"
                v-model="detail"
              ></v-textarea>
            </v-col>
          </v-row>
        </v-container>
        <small>*：入力必須</small>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          color="blue darken-1"
          text
          @click="cancel"
        >
          Close
        </v-btn>
        <v-btn
          color="blue darken-1"
          text
          @click="fix"
        >
          Save
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props:{
    show: Boolean,
    todo: Object
  },
  methods:{
    fix(){
      this.$emit('doUpdate', {
        title: this.title,
        detail: this.detail
      })
    },
    cancel(){
      this.$emit('cancel');
    }
  },
  data(){
    return {
      title: "",
      detail: ""
    }
  },
  watch:{
    // 状態の監視（function名＝$data名となっている）
    show(newShow){
      if (newShow){
        // 非表示から表示になったときに初期化する
        this.title = this.todo.title;
        this.detail = this.todo.detail;
      }
    }
  }
}
</script>

<style>

</style>