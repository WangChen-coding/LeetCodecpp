创建三个链表 分别管理大于等于小于三组，然后再将三组内容连接起来。

```cpp
list_node * list_partition(list_node * head, int pivot)
{
    //////在下面完成代码
    list_node* sh=NULL;
    list_node* st=NULL;
    list_node* eh=NULL;
    list_node* et=NULL;
    list_node* dh=NULL;
    list_node* dt=NULL;
    list_node* next=NULL;
    while(head!=NULL){
        next=head->next;
        head->next=NULL;//此处的处理是把节点单独拿出来，防止把链表全接上去
        if(head->val<pivot){
            if(sh!=NULL){
                st->next=head;
                st=head;
            }else{
                sh=head;
                st=head;
            }
        }else if(head->val==pivot){
            if(eh!=NULL){
                et->next=head;
                et=head;
            }else{
                eh=head;
                et=head;
            }
        }else{
            if(dh!=NULL){
                dt->next=head;
                dt=head;
            }else{
                dh=head;
                dt=head;
            }
        }
        head=next;
    }
    if(sh!=NULL){
        if(eh!=NULL){
            st->next=eh;
            et->next=dh;
        }else{
            st->next=dh;
        }
        return sh;
    }else{
        if(eh!=NULL){
            et->next=dh;
            return eh;
        }else{
            return dh;
        }
    }
}
```

需要注意的点就是把head断开，再接入到对应的链表中，接入完成后再获取后面的值，避免原链表全部接入，还需要更加复杂的处理。