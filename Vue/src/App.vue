<template>
  <div class="content">
    <h1 class="digitastic">Digitastic.Plus</h1>
    <form @submit.prevent="addTodo">
      <div class="field">
        <label class="label">Add New Link</label>
        <div class="control">
          <input
            v-model="todo"
            class="inputUrl"
            type="text"
            placeholder="link url: www.abc.xyz"
          />&nbsp;
          <input
            v-model="nameInput"
            class="inputName"
            type="text"
            placeholder="Name"
          />&nbsp;
          <button type="submit" class="button is-warning is-small">Add</button>
        </div>
        <div id="snackbar">Added Succesfuly.</div>
        <div id="snackbarRemove">Removed Succesfuly.</div>
      </div>
      <button class="button is-small" @click="sortHighestArray()">
        Order By Highest Vote
      </button>
      <button class="button is-small" @click="sortLowestArray()">
        Order By Lowest Vote
      </button>
    </form>

    <div v-for="(value, index) in todos" :key="value.id" class="card my-5 mx-5">
      <div class="card-content">
        <div class="media">
          <div class="media-left"></div>
          <div class="media-content">
            <p class="title is-4 cursor">
              <span class="urlTitle" style="font-weight: lighter">Url : </span
              >{{ value.content }}
            </p>
            <p class="subtitle is-6">Name : {{ value.name }}</p>
            <p class="subtitle is-6">
              <button class="button is-small" @click="add(value)">
                Up Vote</button
              >&nbsp;<button class="button is-small" @click="sub(value)">
                Down Vote
              </button>
              Vote :
              {{ value.vote }}
            </p>
            <button
              class="button is-danger is-small"
              @click="deleteTodo(index)"
            >
              Delete
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const todo = ref("");
    const nameInput = ref("");
    const todos = ref([]);
    const selected = ref("Select Sort");
    todos.value = JSON.parse(window.localStorage.getItem("card"));

    function addTodo() {
      if (todo.value != "") {
        todos.value.push({
          content: todo.value,
          id: Date.now(),
          vote: 0,
          name: nameInput.value,
        });
        window.localStorage.setItem("card", JSON.stringify(todos.value));
        var x = document.getElementById("snackbar");
        x.className = "show";
        setTimeout(function () {
          x.className = x.className.replace("show", "");
        }, 3000);
      }

      todo.value = "";
      nameInput.value = "";
    }
    function add(todo) {
      todo.vote++;
      window.localStorage.setItem("card", JSON.stringify(todos.value));
    }
    function sub(todo) {
      todo.vote--;
      window.localStorage.setItem("card", JSON.stringify(todos.value));
    }
    function deleteTodo(index) {
      if (confirm("Are you sure?") == true) {
        todos.value.splice(index, 1);
        window.localStorage.setItem("card", JSON.stringify(todos.value));
        var x = document.getElementById("snackbarRemove");
        x.className = "show";
        setTimeout(function () {
          x.className = x.className.replace("show", "");
        }, 3000);
      }
    }
    function sortHighestArray() {
      /* index.vote.sort(function (a, b) {
        return a - b;
      }); */
      todos.value.sort((a, b) => b.vote - a.vote);
      console.log(todos.value.sort((a, b) => b.vote - a.vote));
    }
    function sortLowestArray() {
      /* index.vote.sort(function (a, b) {
        return a - b;
      }); */
      todos.value.sort((a, b) => a.vote - b.vote);
      console.log(todos.value.sort((a, b) => a.vote - b.vote));
    }
    return {
      todo,
      nameInput,
      todos,
      selected,
      addTodo,
      sub,
      add,
      deleteTodo,
      sortHighestArray,
      sortLowestArray,
    };
  },
};
</script>

<style lang="scss">
.content {
  margin: auto;
  width: 50%;
  border: 3px solid rgb(4, 247, 4);
  padding: 10px;
}
.digitastic {
  text-align: center;
}
</style>
<style>
#snackbarRemove {
  visibility: hidden;
  min-width: 250px;
  margin-left: -125px;
  background-color: rgb(96, 209, 51);
  color: #fff;
  text-align: center;
  border-radius: 2px;
  padding: 16px;
  position: fixed;
  z-index: 1;
  left: 50%;
  bottom: 30px;
  font-size: 17px;
}

#snackbarRemove.show {
  visibility: visible;
  -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s;
  animation: fadein 0.5s, fadeout 0.5s 2.5s;
}

@-webkit-keyframes fadein {
  from {
    bottom: 0;
    opacity: 0;
  }
  to {
    bottom: 30px;
    opacity: 1;
  }
}

@keyframes fadein {
  from {
    bottom: 0;
    opacity: 0;
  }
  to {
    bottom: 30px;
    opacity: 1;
  }
}

@-webkit-keyframes fadeout {
  from {
    bottom: 30px;
    opacity: 1;
  }
  to {
    bottom: 0;
    opacity: 0;
  }
}

@keyframes fadeout {
  from {
    bottom: 30px;
    opacity: 1;
  }
  to {
    bottom: 0;
    opacity: 0;
  }
}
</style>
<style>
#snackbar {
  visibility: hidden;
  min-width: 250px;
  margin-left: -125px;
  background-color: rgb(96, 209, 51);
  color: #fff;
  text-align: center;
  border-radius: 2px;
  padding: 16px;
  position: fixed;
  z-index: 1;
  left: 50%;
  bottom: 30px;
  font-size: 17px;
}

#snackbar.show {
  visibility: visible;
  -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s;
  animation: fadein 0.5s, fadeout 0.5s 2.5s;
}

@-webkit-keyframes fadein {
  from {
    bottom: 0;
    opacity: 0;
  }
  to {
    bottom: 30px;
    opacity: 1;
  }
}

@keyframes fadein {
  from {
    bottom: 0;
    opacity: 0;
  }
  to {
    bottom: 30px;
    opacity: 1;
  }
}

@-webkit-keyframes fadeout {
  from {
    bottom: 30px;
    opacity: 1;
  }
  to {
    bottom: 0;
    opacity: 0;
  }
}

@keyframes fadeout {
  from {
    bottom: 30px;
    opacity: 1;
  }
  to {
    bottom: 0;
    opacity: 0;
  }
}
</style>
