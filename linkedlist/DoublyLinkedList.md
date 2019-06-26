# 双向链表例子

```js
class Node {
    constructor(element) {
        this.element = element;
        this.prev = null;
        this.next = null;
    }
}

class DoublyLinkedList {

    constructor() {
        //双向链表的长度
        this.length = 0;
        //双向链表的头结点，初始化为null
        this.head = null;
        //双向链表的尾结点，初始化为null
        this.tail = null;
    }

    // 向链表尾部添加元素
    append(element) {
        let node = new Node(element);

        if (this.head === null) {
            this.head = node;
            this.tail = node;
        } else {
            let previous;
            let current = this.head;

            while (current.next) {
                current = current.next;
            }

            current.next = node;
            node.prev = current;
            this.tail = node;
        }

        this.length++;
        return node;
    }

    // 向链表中插入某个元素
    insert(position, element) {
        if (position >= 0 && position <= this.length) {

            let node = new Node(element);
            let index = 0;
            let previous;
            let current = this.head;

            if (position === 0) {

                if (this.head === null) {
                    this.head = node;
                    this.tail = node;
                } else {
                    current.prev = node;
                    node.next = current;
                    this.head = node;
                }
            } else if (position === this.length) {

                current = this.tail;
                current.next = node;
                node.prev = current;
                this.tail = node;
            } else {

                while (index++ < position) {
                    previous = current;
                    current = current.next;
                }

                previous.next = node;
                node.prev = previous;
                current.prev = node;
                node.next = current;
            }

            this.length++;
            return true;
        } else {
            return false;
        }
    }

    removeAt(position) {
        if (position > -1 && position < this.length) {
            let current = this.head;
            let index = 0;
            let previous;

            if (position === 0) {
                this.head = current.next;

                if (this.length === 1) {
                    this.tail = null;
                    this.head.prev = null;
                }
            } else if (position === this.length - 1) {
                current = this.tail;
                this.tail = current.prev;
                this.tail.next = null;
            } else {
                while (index++ < position) {
                    previous = current.prev;
                    current = current.next;
                }
                previous.next = current.next;
                current.next.prev = previous;
            }

            this.length--;
            return current.element;
        } else {
            return false;
        }
    }
    showHead() {
        return this.head;
    }

    showLength() {
        return this.length;
    }

    showTail() {
        return this.tail;
    }
};

var b = new DoublyLinkedList();
b.append(2)

console.log(b);
console.log(b.showHead());
console.log(b.showLength());
```