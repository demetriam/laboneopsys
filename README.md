# laboneopsys

// list/list.c
// 
// Implementation for linked list.
//
// <Author>

#include <stdio.h>
#include <stdlib.h>
//#include <string.h>

#include "list.h"

// allocate heap memory for a linked list 
list_t *list_alloc() { 
  list_t* list = (list_t*) malloc(sizeof(list_t));
  list->head = NULL;
  return list; 
} 
node_t *node_alloc(elem val){
  node_t* new_node = (node_t*) malloc(sizeof(node_t));
  new_node->value = val;
  new_node->next = NULL;
  return new_node;
}

char toString(list_t *l){
  char temp[250];
  
}
// Free heap memory from a linked list 
void list_free(list_t *l) {
  node_t *ptr = l->head;
  if (ptr == NULL)
    printf("Linked list is empty");
    
  while(ptr != NULL) {
    node_t *temp = ptr -> next;
    free(ptr);
    ptr = temp;
  }

}


// print out the linked list 
void list_print(list_t *l) {
  node_t *ptr = l->head;
  if (ptr == NULL)
      printf("Linked list is empty");

  while(ptr != NULL) {
    ptr = ptr -> next; 
  }
}
 
  
 // return the length of the list 
int list_length(list_t *l) { 
  int count = 0;
  node_t *ptr = l->head;
   while(ptr != NULL)
   {
     count ++;
     ptr = ptr->next; 
   }
   return count; 
 }


// 
void list_add_to_back(list_t *l, elem value) {
  node_t *new_node;
  node_t *ptr = l->head;
  new_node = node_alloc(value);
  if (ptr == NULL)
      printf("Linked list is empty");

  while(ptr-> next != NULL)
  { 
    ptr = ptr -> next;    
  }
  ptr->next = new_node;
  new_node->next = NULL;
}

void list_add_to_front(list_t *l, elem value) {
  node_t *new_node;
  new_node = node_alloc(value);
  node_t *head = l->head;
  new_node->next = head; // added a node in fron to head
  l->head = new_node;
  // node_t type of node and list_t is the type of the list list_t can the head 
  // node_t is the value and next  
}

void list_add_at_index(list_t *l, elem value, int index) 
{
  int count = 0;
  node_t *ptr = l->head;
  node_t *prev = NULL;
  node_t *new_node;
  new_node = node_alloc(value);
  
  if (index == 0 )
    return list_add_to_front(l, value);
    
  if (ptr == NULL)
  
  while(count < index)
  { 
    prev = ptr;
    ptr = ptr->next;
    count ++;
    
  }
  prev->next = new_node;
  new_node->next = ptr;
  
}

elem list_remove_from_back(list_t *l) { 
  node_t *ptr = l->head;
  if (ptr == NULL)
    return ;
  while(ptr-> next != NULL)
  { 
    ptr = ptr->next;
  }
  
  elem last_val = ptr->value;
  free(ptr);  
  return last_val; }


elem list_remove_from_front(list_t *l) { 
  if(!l){
    printf("Linked list is empty");
    return;  
  }
  elem to_remove = l->head->value ; 
  node_t *front = l->head;
  l->head = l->head->next;
  free(front);
  return to_remove; 
  
}

elem list_remove_at_index(list_t *l, int index) { 
  node_t *ptr = l->head;
  if (ptr == NULL)
    printf("Linked list is empty");
    return ;
  int count = 0; 
  node_t *temp = l->head;
  while(temp->next != NULL && count < index ){
    temp = temp->next;
    count ++; 
  }
  
  node_t *to_remove = temp->next;
  elem val = temp->next->value;
  temp-> next = temp->next->next;
  free(to_remove);
  return val; 
    
}

bool list_is_in(list_t *l, elem value) { 
  node_t *current = l->head;
  while(current != NULL){
    if(current->value == value){
      return true;
    }
    current = current->next;
  }
  return false; }

elem list_get_elem_at(list_t *l, int index) { 
  int i = 0; 
  node_t *current = l->head;
  while (current != NULL){
    if( i == index){
      return current->value;
    }
    current = current->next;
    i = i+1;
  }
  return -1; 
}


int list_get_index_of(list_t *l, elem value) { 
  int count = 0; 
  node_t *ptr = l->head;
  if (ptr == NULL)
    return ;
  while(ptr != NULL) {
    if (ptr->value == value){
      return count; }
    count ++;
    ptr = ptr -> next;   
  }
  return -1; 
}


