# Data-structure-partical-program-11
class Node:
    def __init__(self,key):
        self.key=key
        self.left=None
        self.right=None
        self.h=1

def height(n):
    if not n: return 0
    return n.h

def rotateRight(y):
    x=y.left
    y.left=x.right
    x.right=y
    y.h=max(height(y.left),height(y.right))+1
    x.h=max(height(x.left),height(x.right))+1
    return x

def rotateLeft(x):
    y=x.right
    x.right=y.left
    y.left=x
    x.h=max(height(x.left),height(x.right))+1
    y.h=max(height(y.left),height(y.right))+1
    return y

def balance(n):
    return height(n.left)-height(n.right)

def insert(root,key):
    if not root: return Node(key)
    if key<root.key:
        root.left=insert(root.left,key)
    else:
        root.right=insert(root.right,key)

    root.h=1+max(height(root.left),height(root.right))
    b=balance(root)

    if b>1 and key<root.left.key:
        return rotateRight(root)
    if b<-1 and key>root.right.key:
        return rotateLeft(root)

    return root

def inorder(root):
    if root:
        inorder(root.left)
        print root.key,
        inorder(root.right)

root=None
root=insert(root,30)
root=insert(root,20)
root=insert(root,40)
root=insert(root,10)

print "Customer Accounts:"
inorder(root)
