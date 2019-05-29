<template>
    <div class="todo">
        <img src="./images/information.png" alt="information" class="todo-information-open" @click="switchInformation()"/>

        <div class="todo-information" :class="{ active : information }">
            <div class="todo-information-container">
                <img src="./images/close.png" alt="close" class="todo-information-close" @click="switchInformation()"/>

                <h1>
                    Todo
                </h1>

                <p></p>

                <p>
                    Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Maecenas porttitor congue massa. Fusce posuere, magna sed pulvinar ultricies, purus lectus malesuada libero, sit amet commodo magna eros quis urna.<br><br>
                    Nunc viverra imperdiet enim. Fusce est. Vivamus a tellus. <br><br>
                    Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Proin pharetra nonummy pede. Mauris et orci. <br><br>
                    Aenean nec lorem. In porttitor. Donec laoreet nonummy augue. <br><br>
                    Suspendisse dui purus, scelerisque at, vulputate vitae, pretium mattis, nunc. Mauris eget neque at sem venenatis eleifend. Ut nonummy. <br><br>
                    Fusce aliquet pede non pede. Suspendisse dapibus lorem pellentesque magna. Integer nulla. <br><br>
                    Donec blandit feugiat ligula. Donec hendrerit, felis et imperdiet euismod, purus ipsum pretium metus, in lacinia nulla nisl eget sapien. Donec ut est in lectus consequat consequat. <br><br>
                    Etiam eget dui. Aliquam erat volutpat. Sed at lorem in nunc porta tristique. <br><br>
                    Proin nec augue. Quisque aliquam tempor magna. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. <br><br>
                    Nunc ac magna. Maecenas odio dolor, vulputate vel, auctor ac, accumsan id, felis. Pellentesque cursus sagittis felis.
                </p>
            </div>
        </div>

        <div class="todo-head">
            <button class="todo-head-button" :class="{ active : view != 'default' }" @click="switchView()">
                <span>+</span>
            </button>

            <h1 class="todo-head-title">
                {{ days[(date.getDay() - 1)] }}, {{ date.getDate() }} {{ months[(date.getMonth())]}}
            </h1>

            <p class="todo-head-count">
                {{ todos.length }} tasks
            </p>
        </div>

        <div class="todo-body" :class="{ active : view == 'default' }" id="default">
            <ul class="todo-body-list">
                <li v-for="(todo, index) in todos" class="todo-body-list-item" :class="{ completed : todo.completed }" :key="todo.id" @click="change(index)">
                    <button class="todo-body-list-item-check"></button>

                    <p class="todo-body-list-item-title">
                        {{ todo.title }}
                    </p>

                    <p class="todo-body-list-item-time">
                        #{{ (index + 1) }}
                    </p>
                </li>
            </ul>
        </div>

        <div class="todo-body" :class="{ active : view == 'add' }" id="add">
            <label for="title" class="todo-body-label">
                title:
            </label>

            <input type="text" name="title" id="title" v-model="todo.title" @keyup.enter="add()" autocomplete="off" class="todo-body-input" placeholder="Please type here a title">
        </div>
    </div>
</template>

<script>
    export default
    {
        name: 'app',

        data()
        {
            return {
                information: false,
                view: 'default',
                date: new Date(),

                months:
                [
                    "January",
                    "February",
                    "March",
                    "April",
                    "May",
                    "June",
                    "July",
                    "August",
                    "September",
                    "October",
                    "November",
                    "December"
                ],

                days:
                [
                    'Monday',
                    'Tuesday',
                    'Wednesday',
                    'Thursday',
                    'Friday',
                    'Saturday',
                    'Sunday'
                ],

                todo:
                {
                    index: 0,
                    title: ''
                },

                todos:
                [
                    {
                        id: 1,
                        title: 'Task one',
                        completed: false
                    },

                    {
                        id: 2,
                        title: 'Task two',
                        completed: false
                    }
                ]
            }
        },

        methods:
        {
            add()
            {
                if(this.todo.title.trim().length > 0)
                {
                    this.todos.push(
                        {
                            id: (this.todos.length + 1),
                            title: this.todo.title,
                            completed: false
                        }
                    );

                    this.switchView();
                }
            },

            change(id)
            {
                this.todos[id].completed = !this.todos[id].completed;
            },

            switchView()
            {
                if(this.view == 'default')
                {
                    this.view = 'add';
                }
                else if(this.view == 'add')
                {
                    this.view = 'default';
                }
            },

            switchInformation()
            {
                this.information = !this.information;
            }
        }
    }
</script>