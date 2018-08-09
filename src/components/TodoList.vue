<template>
	<div class="todo-list">
		<!--<form>-->
		<div class="todo-list-head">
			<label for="NewTodoText">
				新增备忘
				<input id="NewTodoText" type="text" v-model="newTodoText" @keydown.enter="add" placeholder="请输入备忘事项">
			</label>
			<button @click="add">添加</button>
		</div>

		<!--</form>-->
		<div class="todo-list-total">
			<ul>
				<li v-for="(item,index) in todoListArr" @click="toggleCurTodoStatus(index)" :key="index">
					<span :class="[item.done?'done':'','single-todo-list-text']">
						{{item.text}}
					</span>
					<button class="del-single-button" @click.stop="delSingle(item)">
						删除
					</button>
				</li>
			</ul>
			<div class="todo-list-bottom">
				<div class="todo-list-num">
					<span>{{todoListArr.length}} 条</span>
				</div>
				<div class="todo-list-btn-group">
					<button @click="refreshTodoListArr('DONELIST')">完成</button>
					<button @click="refreshTodoListArr('DOINGLIST')">未完成</button>
					<button @click="refreshTodoListArr('TOTALLIST')">全部</button>
				</div>
			</div>
		</div>

	</div>
</template>

<script>


    export default {
        name: "TodoList",
        data() {
            return {
                newTodoText: "",
                todoListArr: [],
                todoListTotalArr: [],
                selectedList: 'TOTALLIST'
            }
        },
        created() {
            this.todoListArr = this.todoListTotalArr
        },
        computed: {},
        methods: {
            add() {
                // console.log(this.todoListArr)
                if (!!this.newTodoText) {
                    this.todoListTotalArr.push({
                        text: this.newTodoText,
                        done: false
                    });
                    this.newTodoText = ""
                    this.refreshTodoListArr(this.selectedList)
                } else {
                    alert("备忘内容不能为空")
                }
            },
            toggleCurTodoStatus(index) {
                this.todoListTotalArr[index].done = !this.todoListTotalArr[index].done
                this.refreshTodoListArr(this.selectedList)
            },
            todoListDoneArr() {
                return this.todoListTotalArr.filter((item, index) => {
                    return item.done === true;
                })
            },
            todoListDoingArr() {
                return this.todoListTotalArr.filter((item, index) => {
                    return item.done === false;
                })
            },
            refreshTodoListArr(list) {
                this.selectedList = list;
                switch (list) {
                    case "DONELIST":
                        this.todoListArr = this.todoListDoneArr();
                        break;
                    case "DOINGLIST":
                        this.todoListArr = this.todoListDoingArr();
                        break;
                    case "TOTALLIST":
                        this.todoListArr = this.todoListTotalArr;
                        break;
                    default:
                        this.todoListArr = []
                }
            },
            delSingle(curitem) {
                this.todoListTotalArr = _.remove(this.todoListTotalArr, (item) => {
                    return item !== curitem;
                });
                this.refreshTodoListArr(this.selectedList)
            }
        }
    }
</script>

<style scoped lang="scss">
	.todo-list {
		width: 400px;
		margin: 0 auto;
		background-color: #ececec;
		padding: 20px;
	}

	.todo-list-head {
		background-color: lightcyan;
		padding: 10px 20px;
	}

	.todo-list-total {
		ul {
			list-style: none;
			padding: 0;
		}
		li {
			display: flex;
			justify-content: space-between;
			align-items: center;
			padding: 10px;
			border-bottom: 1px solid #000;
		}
		.single-todo-list-text {
			flex: 9;

		}
		.single-todo-list-text.done {
			text-decoration: line-through;
		}

		.del-single-button {
			flex: 1;
		}

		.todo-list-bottom {
			display: flex;
			justify-content: space-between;
			align-items: center;
			.todo-list-num {

			}
			.todo-list-btn-group {
				flex: 3;
				> button {
					float: right;
				}
			}
		}

	}
</style>