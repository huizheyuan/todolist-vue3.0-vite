<template>
    <div class="viewWrapper">
        <h1 class="center">Personal Home</h1>
        <section class="operation">
            <input v-model="planCon" class="inputStyle" type="text" placeholder="计划内容" />
            <button @click="addPlan(index)" class="buttonStyle primaryBtn">新增计划</button>
        </section>
        <div class="content">
            <section class="listCon customScroll">
                <h3 class="listTitle">TO DO LIST</h3>
                <ul>
                    <li class="listItem" v-for="(item, index) in list.todolist" :key="index">
                        <span>{{ index + 1 }}、{{ item.title }}</span>
                        <button @click="finish(index)" class="fr buttonStyle successBtn">完成</button>
                    </li>
                </ul>
            </section>
            <section class="listCon customScroll">
                <h3 class="listTitle">DONE LIST</h3>
                <ul>
                    <li class="listItem" v-for="(item, index) in list.donelist" :key="index">
                        <span>{{ index + 1 }}、{{ item.title }}</span>
                        <button @click="cancel(index)" class="fr buttonStyle">取消</button>
                    </li>
                </ul>
            </section>
        </div>
    </div>
</template>

<script>
import { ref, reactive } from 'vue'
export default {
    name: 'App',
    setup() {
        let { list, planCon, finish, cancel, addPlan } = myList()
        return { list, planCon, finish, cancel, addPlan }
    }
}

function myList() {
    let list = reactive({
        todolist: [
            { id: 1, title: '学习 vue3.0' },
            { id: 2, title: '学习 typescript' }
        ],
        donelist: [
            { id: 1, title: '吃鸡' }
        ]
    })
    let planCon = ref('')
    function finish(indx) {
        list.todolist.map((e, index) => {
            if (index === indx) {
                list.donelist.push(e)
                list.todolist.splice(index, 1)
            }
        })
    }
    function cancel(indx) {
        list.donelist.map((e, index) => {
            if (index === indx) {
                list.todolist.push(e)
                list.donelist.splice(index, 1)
            }
        })
    }
    function addPlan(e) {
        let uUid = 0
        if (planCon.value === '') return
        list.todolist.unshift({
            id: uUid++,
            title: planCon.value
        })
        planCon.value = ''
        alert('添加成功')
    }
    return { list, planCon, finish, cancel, addPlan }
}
</script>

<style lang='css' scoped>
.operation {
    margin: 20px;
}
.content {
    display: flex;
}
.content > .listCon {
    flex: 1;
    border: 1px solid #dcdee2;
    border-color: #e8eaec;
    border-radius: 4px;
    font-size: 14px;
    margin: 20px;
    padding: 20px;
    height: 600px;
    overflow-y: scroll;
}
.content .listTitle {
    padding: 10px;
}
.content .listItem {
    border-radius: 4px;
    padding: 20px;
    line-height: 30px;
}
.content .listItem:hover {
    box-shadow: 0 1px 6px rgba(0, 0, 0, 0.2);
    border-color: #eee;
}
</style>