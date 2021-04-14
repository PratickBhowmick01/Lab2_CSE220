# Lab2_CSE220
Class Node, Class LinkedList

#Lab2
class Node:
    def __init__(self, value, next):
        self.value = value
        self.next = next

    def printNode(self):
        print(self.value, end = " ")

    def printNode2(self, head):
        n = head
        while (n != None):
            print(n.value, end = " ")
            n = n.next
        print()


#==================================================================

class MyList:

    def __init__(self, a = None):  #list from an array
        self.head = None
        tail = None

        if(type(a) is list):
            for i in a:
                n = Node(i, None)   #creating a node
                if(self.head == None):
                    self.head = n
                    tail = n
                else:
                    tail.next = n
                    tail = n

        elif(type(a) == MyList):   #list from a list
            self.head = None
            tail = None
            n = a.head
            while (n != None):
                newNode = Node(n.value,None)
                if (self.head == None):
                    self.head = newNode
                    tail = newNode
                else:
                    tail.next = newNode
                    tail = newNode
                n = n.next

    def showList(self): 
        if (self.head == None):
            print("Empty list")
        else:
            n = self.head
            while(n != None):
                print(n.value, end = " ")
                n = n.next

    def isEmpty(self):
        if(self.head == None):
            return True
        else:
            return False

    def clear(self):
        self.head = None

    def insert(self, newElement, index = None):

        if(index == None):
            n = self.head
            new_n = Node(newElement, None)
            while(n != new_n):
                if(n.value == newElement):
                    break
                elif(n.next == None):
                    n.next = new_n
                    n = n.next
                else:
                    n = n.next

        else:
            new_n = Node(newElement, None)
            n = self.head
            char = ""
            while(n != None):                 #checking for similar value
                if(n.value == newElement):
                    char = "Invalid"
                    break
                n = n.next

            n = self.head
            tail = n
            count = 0
            if(char != "Invalid" and index >= 0):   #inserting
                while(n != None):
                    if(count == index):
                        tail.next = new_n
                        new_n.next = n
                    count += 1
                    tail = n
                    n = n.next

    def remove(self, deletekey):
        n = self.head
        tail = n
        count = 0
        while(n != None):
            if(n.value == deletekey):
                if(count == 0):
                    self.head = n.next
                    return n.value
                else:
                    tail.next = n.next
                    return n.value
            count += 1
            tail = n 
            n = n.next

    def findEven(self, a):
        newH = None
        newT = None
        n = a.head
        while (n != None):
            if(n.value % 2 == 0):
                newNode = Node(n.value, None)
                if (newH == None):
                    newH = newNode
                    newT = newNode
                else:
                    newT.next = newNode
                    newT = newNode
            n = n.next
        newH.printNode2(newH)   #printing using head reference
        
    def findElement(self, elem):
        n = self.head
        while (n != None):
            if (n.value == elem):
                return True
                break
            n = n.next
        return False
    
    def reverseList(self, a):
        newH = None
        n = a.head
        while(n != None):
            nextNode = n.next
            n.next = newH
            newH = n
            n = nextNode 
        newH.printNode2(newH)
        
    def sort(self, a):
        n = a.head
        count = a.head 
        while(n != None):
            min_v = n.value 
            
            while(count != None):     #swapping with minm value
                if(count.value < min_v):
                    copy = min_v
                    min_v = count.value
                    count.value = copy
                count = count.next 
                
            n.value = min_v
            n = n.next 
            count = n         
        a.showList()
        
    def sumValues(self, a):
        n = a.head
        total = 0
        while(n != None):
            total += n.value
            n = n.next
            
        print(total)
        
    def rotate(self, direction, a, k): 
        if(direction == "left"):
            i = 1
            while(i <= k):
                oldH = a.head  
                newH = oldH.next
                tail = newH 
                
                while(tail.next != None):
                    tail = tail.next
                    
                tail.next = oldH 
                oldH.next = None 
                self.head = newH 
                i += 1
                
            self.head.printNode2(self.head)   #printing with head reference 
            
        else:
            i = 1
            while(i <= k):
                oldH = a.head
                newH = None  
                tail = oldH 
                count = 1
                while(tail.next != None):  #finding the tail
                    tail = tail.next
                    count += 1
                    
                newH = tail 
                newH.next = oldH                  
                test = 1
                while(test < count-1):  #removing previous link to tail
                    oldH = oldH.next
                    test += 1
                oldH.next = None 
                
                self.head = newH 
                i += 1          
            self.head.printNode2(self.head) 
    
    #other
    def printDuplicate(self, a):
        n = a.head
        
        while(n.next != None):
            dup = n.value 
            check = n.next
            while(check != None):       #checking duplicates
                if(dup == check.value):
                    return dup
                check = check.next             
            n = n.next
            
        return "No duplicates"
    #other
    def remove_multiple_of_five(self,a):
        
        n = a.head 
        tail = n
        count = 0
        while(n != None):
            if(n.value % 5 == 0):
                if(count == 0):
                    self.head = n.next  
                    count -= 1 
                
                else:
                    tail.next = n.next 
                    n = tail
            tail = n 
            n = n.next
            count += 1
            
        # self.head = head
        # head.printNode2(head)  
    
list1 = [4,5,3]   
list2 = MyList(list1)
list2.remove_multiple_of_five(list2)
list2.showList()  
# print("Before method: ", end = "")
# list2.showList()
# print()  
# print("After method: ", end = "")  
#required method to be called 
# list3 = list2.rotate("right", list2, 2)
# print(list2.printDuplicate(list2))
