#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Thu May 13 04:27:46 2021

@author: chanonboonkangwan
"""

import matplotlib.pyplot as plt
#import random;
import sympy;
class OAHashTable:
    class Entry:
       def __init__(self,k,v):
            self.key = k; self.value = v;

    def __init__(self,m):
        self.table = [None]*m;
        self.size = 0;
        self.DELETE = self.Entry(object(),None);
        self.numExistCells = 0;

    def __indexOf(self,key):
        hI = self.__h(key);
        for j in range(len(self.table)):
            e = self.table[hI];
            if(e == None or e.key == key): return hI;
            hI = (hI + 1) % len(self.table);
            
    def __h(self,key):
        key = str(key);
        return (abs(hash(key)))% len(self.table)

    def length(self): return self.size;

    def display(self):
        x,y = [],[];
        for i in range(len(self.table)):
            x.append(i);
            e = self.table[i]
            if(e != None and e != self.DELETE): y.append(1);
            else: y.append(0);
        print("n = ",self.size,"m=",len(self.table),"lambda",self.size/len(self.table));
        plt.bar(x,y,align='edge', width=1);
        plt.show();
    

    def get(self,key):
        hI = self.__indexOf(key);
        e = self.table[hI];
        return None if (e == None or e == self.DELETE) else e.value;

    def put(self,k,v):
        empty = -1;
        oldValue = None;
        hI = self.__h(k);
        
        for j in range(len(self.table)):
            e = self.table[hI]
            if(e == self.DELETE and empty == -1): empty = hI;
            if(e == None or e.key == k): break;
            hI = (hI + 1) % len(self.table);
        
        if(self.table[hI] == None):
            if(empty != -1): hI = empty;
            self.table[hI] = self.Entry(k,v);
            self.size += 1;
            if(empty == -1): self.numExistCells += 1;
            if(self.numExistCells > len(self.table)/2): self.rehash();
            
        elif(self.table[hI].key == k):
            oldValue = self.table[hI].value;
            self.table[hI].value = v;

        return oldValue;

    def remove(self,key):
        hI = self.__indexOf(key);
        if(self.table[hI] != None):
            self.table[hI] = self.DELETE;
            self.size -= 1;

    def rehash(self):
        oldTable = self.table
        self.table = [None] * self.size * 4
        self.size = self.numExistCells = 0;
        for i in range(len(oldTable)):
            entry = oldTable[i]
            if(entry != None and entry != self.DELETE):
                self.put(entry.key,entry.value)
    

class OAQDHashTable(OAHashTable):
    def __init__(self,m):
        self.size = 0;
        self.DELETE = self.Entry(object(),None);
        self.numExistCells = 0;
        self.table = [None] * self.__nextPrime(m);
        
    def __nextPrime(self,n): return sympy.nextprime(n);

    def __h(self,key):
        key = str(key);
        return (abs(hash(key)))% len(self.table)
    
    def rehash(self):
        oldTable = self.table
        self.table = [None] * self.__nextPrime(self.size)* 4
        self.size = self.numExistCells = 0;
        for i in range(len(oldTable)):
            entry = oldTable[i]
            if(entry != None and entry != self.DELETE):
                self.put(entry.key,entry.value)
        
    def __indexOf(self,key):
        hI = self.__h(key);
        for j in range(len(self.table)):
            e = self.table[hI];
            if(e == None or e.key == key): return hI;
            hI = (hI + 2*j - 1) % len(self.table);
            
    def put(self,k,v):
        empty = -1;
        oldValue = None;
        hI = self.__h(k);
        
        for j in range(len(self.table)):
            e = self.table[hI]
            if(e == self.DELETE and empty == -1): empty = hI;
            if(e == None or e.key == k): break;
            hI = (hI + 2*j-1) % len(self.table);
        
        if(self.table[hI] == None):
            if(empty != -1): hI = empty;
            self.table[hI] = self.Entry(k,v);
            self.size += 1;
            if(empty == -1): self.numExistCells += 1;
            if(self.numExistCells > len(self.table)/2): self.rehash();
            
        elif(self.table[hI].key == k):
            oldValue = self.table[hI].value;
            self.table[hI].value = v;

        return oldValue;

class OADBHashTable(OAQDHashTable):
    def __init__(self,m):
        self.size = 0;
        self.DELETE = self.Entry(object(),None);
        self.numExistCells = 0;
        self.table = [None] * self.__nextPrime(m);

        
    def __nextPrime(self,n): return sympy.nextprime(n);

    def __h(self,key):
        key = str(key);
        return (abs(hash(key)))% len(self.table)
    
    def __g(self,key):
        key = str(key);
        return 13 - (abs(hash(key)))% 13

    def __indexOf(self,key):
        hI = self.__h(key);
        g = self.__g(key);
        for j in range(len(self.table)):
            e = self.table[hI];
            if(e == None or e.key == key): return hI;
            hI = (hI + g) % len(self.table);
            
    def put(self,k,v):
        empty = -1;
        oldValue = None;
        hI = self.__h(k);
        g = self.__g(k);
        
        for j in range(len(self.table)):
            e = self.table[hI]
            if(e == self.DELETE and empty == -1): empty = hI;
            if(e == None or e.key == k): break;
            hI = (hI + g) % len(self.table);
        
        if(self.table[hI] == None):
            if(empty != -1): hI = empty;
            self.table[hI] = self.Entry(k,v);
            self.size += 1;
            if(empty == -1): self.numExistCells += 1;
            if(self.numExistCells > len(self.table)/2): self.rehash();
            
        elif(self.table[hI].key == k):
            oldValue = self.table[hI].value;
            self.table[hI].value = v;

        return oldValue;

    
data = [ (i,i) for i in range(1000) ];
        
oh1 = OAHashTable(600);
oh2 = OAQDHashTable(600);
oh3 = OADBHashTable(600);
#oh.put("name","CHANON");
#oh.put("name2","NICKY");
#oh.put("name3","6105290");

for e in data:
    oh1.put(e[0],e[1]);
    oh2.put(e[0],e[1]);
    oh3.put(e[0],e[1]);


oh1.display()
oh2.display()
oh3.display()


