# Dva 路由切换重置model的state


好多业务场景需要用到当页面A离开再回来时候需要清空A页面的状态数据，以下是一个代码栗子


```js

// 在model.js中修改

const initalState = {
    a: 1,
    b: 2,
}


export default {
    namespace: 'myNameSpace',
    state: {
        ...initalState
    },
    subscriptions: {
        setup({ dispatch, history }) {
            history.listen((location) => {
                /**
                 * 监听路由变化
                 */
                if (location.pathname == "/xxxxxx") {
                    // 重置当前页面state
                    dispatch({
                        type: 'initalState'
                    });
                }
            });
        }
    },
    effects: {},
    reducers: {
        initalState(state, action){
            return {
                ...initalState,
            };
        },
    }
};

```
