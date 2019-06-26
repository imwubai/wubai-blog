# 单向链表例子

```js
class Node {
    constructor(element) {
        this.element = element;
        this.next = null;
    }
}

class SinglyLinkedList {

    constructor() {
        // 单向链表的长度
        this.length = 0;
        // 单向链表的头结点，初始化为null
        this.head = null;
    }

    // 向单向链表尾部添加元素
    append(element) {
        let node = new Node(element);
        let current;

        if (this.head == null) {
            this.head = node;
        } else {
            current = this.head;
            while (current.next) {
                current = current.next;
            }
            current.next = node;
        }
        this.length++;
    }

    // 要移除元素的位置
    // 移除成功返回被移除的元素，不成功则返回NULL
    removeAt(position) {
        if (position > -1 && position < this.length) {
            let current = this.head;
            let previous;
            let index = 0;

            if (position == 0) {
                this.head = current.next;
            } else {
                while (index++ < position) {
                    previous = current;
                    current = current.next;
                }

                previous.next = current.next;
            }

            this.length--;

            return current.element;
        } else {
            return null;
        }
    }

    // 要插入的位置 要插入的元素
    // 插入成功返回true，失败返回false
    insert(position, element) {

        position = parseInt(position);

        if (Number.isNaN(position)) {
            return false;
        }

        if (position >= 0 && position <= this.length) {
            let node = new Node(element);
            let current = this.head;
            let previous;
            let index = 0;

            if (position == 0) {
                node.next = current;
                this.head = node;
            } else {
                while (index++ < position) {
                    previous = current;
                    current = current.next;
                }

                previous.next = node;
                node.next = current;
            }

            this.length++;
            return true;
        } else {
            return false;
        }
    }

    // 将链表所有内容以字符串输出
    toString() {
        let current = this.head;
        let string = '';

        while (current) {
            string += current.element;
            current = current.next;
        }
        return string;
    }

    // 要寻找的元素,返回值>=0则代表找到相应位置
    indexOf(element) {
        let current = this.head;
        let index = 0;

        while (current) {
            if (element === current.element) {
                return index;
            }
            index++;
            current = current.next;
        }

        return -1;
    }

    // 要移除的元素,返回值>=0表示移除成功
    remove(element) {
        let index = this.indexOf(element);
        return this.removeAt(index);
    }

    // 判断单向链表是否为空
    isAmpty() {
        return this.length === 0
    }

    // 返回单向链表长度
    size() {
        return this.length;
    }

    // 获取单向链表的头部
    getHead() {
        return this.head;
    }
}


let a = new SinglyLinkedList()
a.insert(0, 1)
a.insert(0, 1)
a.insert(0, 4)
a.insert(0, 3)
a.insert('1', 2)
a.append('aaa')


console.log(a);
console.log(a.toString());
console.log(a.size());
console.log(a.getHead());
```