<template>

    <div id="app">
        <div class="container">

            <h1 class="text-center">
                Todo
            </h1>

            <input
                type="text"
                class="form-control mb-4"
                v-model="userInput"
                @keyup.enter="addNewTodo">
                <div class="list-group mb-4">
                    <template>

                        <button
                            class="list-group-item"
                            v-for="todo in activeTodoList"
                            @click="toggleTodoState(todo)"
                            v-bind:key="todo">
                            {{ todo.label }}
                        </button>

                    </template>

                </div>

                <div class="text-right">

                    <button type="button" class="btn btn-sm" @click="changeCurrentState('active')">
                        할일
                    </button>
                    <button type="button" class="btn btn-sm" @click="changeCurrentState('done')">
                        완료
                    </button>
                    <button type="button" class="btn btn-sm" @click="changeCurrentState('all')">
                        전체
                    </button>

                </div>

            </div>
        </div>
    </template>

    <script>
        export default {
            name: 'app',

            data() {
                return {userInput: '', todoList: [], currentState: 'active'};
            },

            methods: {
                addNewTodo() {
                    this
                        .todoList
                        .push({label: this.userInput, state: 'active'});
                    this.userInput = '';
                },

                toggleTodoState(todo) {
                    todo.state = todo.state === 'active'
                        ? 'done'
                        : 'active';
                }
            },

            computed: {
                activeTodoList() {
                    return this
                        .todoList
                        .filter(
                            todo => this.currentState === 'all' || todo.state === this.currentState
                        );
                }
            },

            changeCurrentState(state) {
                this.currentState = state;
            },

            components: {}
        }
    </script>

    <style>
        #app {
            font-family: Avenir, Helvetica, Arial, sans-serif;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            text-align: center;
            color: #2c3e50;
            margin-top: 60px;
        }
    </style>