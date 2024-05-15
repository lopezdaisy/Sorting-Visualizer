# Sorting Visualizer

![Project Image](https://github.com/shubh67678/sorting-visualizer/blob/master/image/gif.gif)
> [Live demo](https://shubh67678.github.io/sorting-visualizer/)

---

## Description

This project helps one to visualize a sorting algorithm. Each element of the array is displayed as a bar. The operations are colour coded such that: 

1. Red - Swap
2. Blue - Comparison 
3. Green - Element is in sorted position

It compares the time taken by the different algorithm for sorting the array.



### Technologies

- HTML 
- CSS
- Javascript (p5.js)

---


## References

Inspiration taken from [coding train](https://www.youtube.com/watch?v=67k3I2GxTH8).

Useful links discribing the algorithms used 

- [Bubble Sort](https://en.wikipedia.org/wiki/Bubble_sort)
- [Selection Sort](https://en.wikipedia.org/wiki/Selection_sort)
- [Merge Sort](https://en.wikipedia.org/wiki/Merge_sort)
- [Quick Sort](https://en.wikipedia.org/wiki/Quicksort)


[Back To The Top](#read-me-template)

---
"""struct LIST * SortList1(struct LIST * pList) 
{
    // zero or one element in list
    if (pList == NULL || pList->pNext == NULL)
        return pList;
    // head is the first element of resulting sorted list
    struct LIST * head = NULL;
    while (pList != NULL) {
        struct LIST * current = pList;
        pList = pList->pNext;
        if (head == NULL || current->iValue < head->iValue) {
            // insert into the head of the sorted list
            // or as the first element into an empty sorted list
            current->pNext = head;
            head = current;
        } else {
            // insert current element into proper position in non-empty sorted list
            struct LIST * p = head;
            while (p != NULL) {
                if (p->pNext == NULL || // last element of the sorted list
                    current->iValue < p->pNext->iValue) // middle of the list
                {
                    // insert into middle of the sorted list or as the last element
                    current->pNext = p->pNext;
                    p->pNext = current;
                    break; // done
                }
                p = p->pNext;
            }
        }
    }
    return head;
}
The algorithm below uses a trailing pointer[10] for the insertion into the sorted list. A simpler recursive method rebuilds the list each time (rather than splicing) and can use O(n) stack space.

struct LIST
{
  struct LIST * pNext;
  int           iValue;
};

struct LIST * SortList(struct LIST * pList)
{
  // zero or one element in list
  if (!pList || !pList->pNext)
      return pList;

  /* build up the sorted array from the empty list */
  struct LIST * pSorted = NULL;

  /* take items off the input list one by one until empty */
  while (pList != NULL) {
      /* remember the head */
      struct LIST *   pHead  = pList;
      /* trailing pointer for efficient splice */
      struct LIST ** ppTrail = &pSorted;

      /* pop head off list */
      pList = pList->pNext;

      /* splice head into sorted list at proper place */
      while (!(*ppTrail == NULL || pHead->iValue < (*ppTrail)->iValue)) { /* does head belong here? */
          /* no - continue down the list */
          ppTrail = &(*ppTrail)->pNext;
      }

      pHead->pNext = *ppTrail;
      *ppTrail = pHead;
  }

  return pSorted;
}"""