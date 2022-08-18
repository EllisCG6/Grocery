<template>
  <main>
    <div class="grocery">
      <header>
        <p class="alert-ok" v-if="added">Item added</p>
        <p class="alert-rau" v-if="removed">Item removed</p>
        <p class="alert-ok" v-if="changed">Item changed</p>
        <p class="alert-rau" v-if="pls">Please add a item</p>
        <h3>Grocery Bud</h3>
      </header>
      <div>
        <input
          v-if="!editB"
          type="text"
          class="input"
          placeholder="e.g. eggs"
          value
          v-model="txt"
          v-on:keyup.enter="submit"
        />
        <input
          v-if="editB"
          type="text"
          class="input"
          placeholder="e.g. eggs"
          value
          v-model="txt"
          v-on:keyup.enter="edit"
        />
        <button v-if="!editB" @click="submit" class="buton">Submit</button>
        <button @click="edit()" class="buton" v-if="editB">Edit</button>
        <section class="list" v-for="(element, index) in arr" :key="index">
          <div class="list-con" v-if="bool">
            <article class="list-item">{{ arr[index] }}</article>
            <div class="btn-container">
              <button @click="editbtn(index)" class="edit-btn">
                <svg
                  stroke="currentColor"
                  fill="currentColor"
                  stroke-width="0"
                  viewBox="0 0 576 512"
                  height="1em"
                  width="1em"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M402.6 83.2l90.2 90.2c3.8 3.8 3.8 10 0 13.8L274.4 405.6l-92.8 10.3c-12.4 1.4-22.9-9.1-21.5-21.5l10.3-92.8L388.8 83.2c3.8-3.8 10-3.8 13.8 0zm162-22.9l-48.8-48.8c-15.2-15.2-39.9-15.2-55.2 0l-35.4 35.4c-3.8 3.8-3.8 10 0 13.8l90.2 90.2c3.8 3.8 10 3.8 13.8 0l35.4-35.4c15.2-15.3 15.2-40 0-55.2zM384 346.2V448H64V128h229.8c3.2 0 6.2-1.3 8.5-3.5l40-40c7.6-7.6 2.2-20.5-8.5-20.5H48C21.5 64 0 85.5 0 112v352c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48V306.2c0-10.7-12.9-16-20.5-8.5l-40 40c-2.2 2.3-3.5 5.3-3.5 8.5z"
                  ></path>
                </svg></button
              ><button @click="sterge(index)" class="delete-btn">
                <svg
                  stroke="currentColor"
                  fill="currentColor"
                  stroke-width="0"
                  viewBox="0 0 448 512"
                  height="1em"
                  width="1em"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M432 32H312l-9.4-18.7A24 24 0 0 0 281.1 0H166.8a23.72 23.72 0 0 0-21.4 13.3L136 32H16A16 16 0 0 0 0 48v32a16 16 0 0 0 16 16h416a16 16 0 0 0 16-16V48a16 16 0 0 0-16-16zM53.2 467a48 48 0 0 0 47.9 45h245.8a48 48 0 0 0 47.9-45L416 128H32z"
                  ></path>
                </svg>
              </button>
            </div>
          </div>
        </section>
      </div>
      <button class="clear-btn" @click="clear">clear</button>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      arr: [],
      k: undefined,
      txt: undefined,
      bool: 0,
      editB: 0,
      pls: 0 /* please enter value */,
      added: 0 /*  item added*/,
      changed: 0 /* item changed */,
      removed: 0 /* item removed */,
      seconds: undefined,
    };
  },
  methods: {
    submit() {
      if (this.txt == " " || !this.txt) {
        this.pls = 1;
        this.removed = 0;
        this.added = 0;
        this.changed = 0;
        clearTimeout(this.seconds);
        this.seconds = setTimeout(() => {
          this.pls = 0;
        }, 3000);
      } else {
        this.arr.push(this.txt);
        this.txt = " ";
        this.bool = 1;
        this.added = 1;
        this.pls = 0;
        this.changed = 0;
        this.removed = 0;
        clearTimeout(this.seconds);
        this.seconds = setTimeout(() => {
          this.added = 0;
        }, 3000);
      }
    },
    editbtn(index) {
      this.txt = this.arr[index];
      this.editB = 1;
      this.k = index;
    },
    sterge(index) {
      this.arr.splice(index, 1);
      this.removed = 1;
      this.added = 0;
      this.pls = 0;
      this.changed = 0;
      clearTimeout(this.seconds);
      this.seconds = setTimeout(() => {
        this.removed = 0;
      }, 3000);
    },
    edit() {
      if (!this.txt) {
        this.pls = 1;
        this.removed = 0;
        this.added = 0;
        this.changed = 0;
        clearTimeout(this.seconds);
        this.seconds = setTimeout(() => {
          this.pls = 0;
        }, 3000);
      } else {
        this.editB = 0;
        this.arr[this.k] = this.txt;
        this.txt = " ";
        this.changed = 1;
        this.added = 0;
        this.pls = 0;
        this.removed = 0;
        clearTimeout(this.seconds);
        this.seconds = setTimeout(() => {
          this.changed = 0;
        }, 3000);
      }
    },
    clear() {
      this.arr = [];
      this.changed = 0;
      this.added = 0;
      this.pls = 0;
      this.removed = 0;
    },
  },
};
</script>

<style>
body {
  background-color: #ebf7ff;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
main {
  display: flex;
  align-items: center;
  justify-content: center;
  align-content: center;
  margin: 5rem auto;
}
.grocery {
  background: white;
  width: 500px;
  display: flex;
  align-items: center;
  flex-flow: column nowrap;
  height: auto;
  border-radius: 0.25rem;
  box-shadow: gray px;
  padding: 2rem;
  transition: all 0.3s linear;
  box-shadow: 0 5px 15px rgb(0 0 0 / 10%);
}
.list-con {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.list-con:hover{
  background-color: rgb(188, 195, 207);
}
.alert-rau{
  background-color:#ebb3b3;
  color:red;
  padding: .25rem
}
.alert-ok{
  background-color:#acecba;
  color:rgb(15, 158, 98);
  text-align: center;
}
.buton {
  background: #a5d5f8;
  border-color: transparent;
  align-items: center;
  padding: 0.20rem;
  letter-spacing: 2px;
  border-top-right-radius: 0.25rem;
  border-bottom-right-radius: 0.25rem;
  cursor: pointer;
  content: #49a6e9;
  transition: all 0.3s linear;
  font-size: 0.85rem;
}
.input {
  background: #f1f5f8;
  color: #617d98;
  border-color: transparent;
  font-size: 1rem;
}
.list-item{
  color: #617d98;
  letter-spacing: 1px;
  text-transform: capitalize;
}
.clear-btn{
  text-transform: capitalize;
    width: 10rem;
    height: 1.5rem;
    display: grid;
    align-items: center;
    background: transparent;
    border-color: transparent;
    color: #e66b6b;
    font-size: .85rem;
    letter-spacing: .1rem;
    cursor: pointer;
    transition: all .3s linear;
    margin: 1.25rem auto 0;
}
.edit-btn{
  color: #6be675;
}
.delete-btn{
  color: #e66b6b;
}
.delete-btn, .edit-btn {
    background: transparent;
    border-color: transparent;
    cursor: pointer;
    font-size: .7rem;
    margin: 0 .15rem;
    transition: all .3s linear;
}
</style>
