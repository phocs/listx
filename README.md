
# listx
It's subset of the Linux 's list implementation.

To use it, `#include <listx.h>"`.

Creating a new listx
---------------------

Data nodes in an listx are structures containing a struct list_head member:

```
typedef struct mydata {
    struct list_head node;
    int key;

    char attr_a;
    char attr_b;
    char attr_c;
    char attr_d;
} mydata_t;
```

At the head of each listx is an list_head structure, which is initialized to be
empty via:
```
struct list_head mylist = LIST_HEAD_INIT(mylist);
// or define and init
LIST_HEAD(mylist)
```
Searching for a value in an listx, example:
-------------------------------------------
```
mydata_t *search(int key, struct list_head *head) {
    mydata_t *data;

    list_for_each_entry(data, head, node) {
        if (data->key == key)
            return data;
    }
    return NULL;
}
```
Inserting data into an listx, example:
--------------------------------------
```
void insert(mydata_t *newdata, struct list_head *head) {
    list_add(&newdata->node, head);
}
```
Removing or replacing existing data in an listx, example:
---------------------------------------------------------
```
void delete(mydata_t *olddata) {
    list_del(&olddata->node);
}

void replace(mydata_t *olddata, mydata_t *newdata) {
    list_replace(&olddata->node, &olddata->node);
}
```

References:
---------------
Linux [Source](https://github.com/torvalds/linux)

Linux List [include/linux/list.h](https://github.com/torvalds/linux/blob/master/include/linux/list.h)
