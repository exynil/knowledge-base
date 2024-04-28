Поиск центра
~~~~python
slow, fast = head, head.next

while fast and fast.next:
	slow = slow.next
	fast = fast.next.next
~~~~