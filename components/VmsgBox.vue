<template>
  <!-- <div class="wrappinv" v-on:click.stop="$emit('changeShow')"> -->
  <div class="overlay" v-on:click="$emit('changeShow')">
    <div class="currentmsg" v-on:click.stop="noChange">
      <!-- <div class="currentmsg" v-show="showTable"> -->

      <div class="tabhead" >
        <button class="btn_icon">
          <img v-on:click="$emit('changeShow')" src="../assets/svg/clear_24px.svg" alt />
          <div class="tabhead_title">Сообщения</div>
        </button>
      </div>
      <div class="bodyTable" >
        <table>
          <tbody>
            <tr v-for="(msg, index) in DevMsgs" :key="index">
              <td width="80%" v-bind:class="msg.status">
                <textarea type="text" readonly v-bind:value="msg.msg" />
              </td>
              <td width="20%" v-bind:class="msg.status">
                <textarea type="text" readonly v-bind:value="msg.msgtime" />
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="tabfoot">
        <button class="tabfoot-left btn_icon">
          <div class="tabfoot_title">Перейти в архив сообщений</div>
        </button>
        <button class="tabfoot-right btn_icon">
          <div class="tabfoot_title">Тактировать сообщение</div>
        </button>
      </div>
    </div>
  </div>
  <!-- </div> -->
</template>
<script>
import { mapGetters } from "vuex";

export default {
  data() {
    return {
      showTable: false
    };
  },
  mounted() {
    this.$store.dispatch('Messages/getCurrentMessages');
  },

  computed: {
    ...mapGetters("Messages", {
      DevMsgs: "currentMessages"
    }),
    dataHead() {
      let statusDev = "ok";
      let alertDev = this.DevMsgs.filter(item => item.status == "alert");
      let dngDev = this.DevMsgs.find(item => item.status == "dng");

      if (dngDev !== undefined) {
        statusDev = "dng";
      } else if (alertDev !== undefined) {
        statusDev = "alert";
      }

      return { title: ``, status: statusDev };
    }
  },
  methods: {
    noChange() {
      1 + 1;
    }
  }
};
</script>

<style scoped>
.overlay {
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.062);
  z-index: 19;
  position: absolute;
  top: 0;
  right: 0;
}

.currentmsg {
  width: 466px;
  max-height: 92vh;
  padding: 0;
  background: #f7f8fa;
  box-shadow: 0px 2px 6px rgba(0, 0, 0, 0.25);

  z-index: 20;

  position: absolute;
  top: 50px;
  right: 0;

  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.btn_icon {

  cursor: pointer;
  background: none;
  border: none;

  display: flex;
  justify-content: baseline;
  outline: none;
}
.bodyTable {

  width: 100%;
  max-height: 95vh;
  overflow: auto;
}

.tabhead_title {
  font-weight: 500;
  font-size: 18px;
  line-height: 22px;
  padding-top: 3px;
  padding-left: 27px;

  color: #4b6075;
}

.tabhead {
  display: flex;
  justify-content: flex-start;
  width: 100%;
  margin-left: -35px;
}
/* img{
    position: relative;
    right:0;
} */

.tabfoot {
  margin-top: 120px;
  width: 100%;
  display: flex;
  flex-direction: row;
}

.tabfoot button {
  cursor: pointer;
  padding: 0;
  width: 233px;
  height: 36px;
}
.tabfoot button:hover {
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.25);
}

.tabfoot-left {
  background-color: hsl(211, 100%, 90%);
}
.tabfoot-left:hover {
  background-color: hsl(211, 100%, 87%);
}
.tabfoot-right {
  background-color: hsl(134, 41%, 88%);
}
.tabfoot-right:hover {
  background-color: hsl(134, 41%, 85%);
}

.tabfoot_title {
  width: 100%;
  font-weight: 500;
  font-size: 14px;
  line-height: 17px;
  padding-top: 9px;
  text-align: center;
}

table {
  margin-top: 24px;
  margin-left: auto;
  margin-right: auto;
  width: 98%;
  border-collapse: collapse;
}
td {

  padding: 0;

  height: 38px;
}

table textarea {
  cursor: pointer;
  padding: 3px 5px;
  background: none;
  border: none;
  outline: none;
  width: 100%;
  height: 36px;
  font-size: 12px;
  line-height: 15px;
  resize: none;
}

table textarea {
  border-left: 4px solid rgba(0, 0, 0, 0);
  /* background: #DEE8FA; */
}

table textarea:hover {
  border-left: 4px solid red;
  /* background: #DEE8FA; */
}

table textarea:focus {
  border-left: 4px solid red;
  /* background: #DEE8FA; */
}

.dng {
  background: #f7dcdf;
  color: #721C24;
}
.alert {
  background: #fff3cd;
  color: #856404;
}
.ok {
  background: #d4edda;
  color: #155724;
}
</style>
