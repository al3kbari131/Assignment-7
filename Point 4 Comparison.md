**Question:** Compare some information relating to collisions (frequency) and their effect on complexity (of insert and contains methods)



**Simple Hashtable:**
 
 Collision is handled by simply replacing the previous value with the new value. On average the insert function complexity will be O(1), as this function 
 will take constant time to execute.
 
    
    void  insert(int key, string value)
    {
        int hashIndex = hashFunction(key);
        table[hashIndex] = new HashNode(key, value);
    }          
The _containsValue()_ method checks the given value in the Hashtable, returns true if it exists and vice versa. All the statements run constant time, 
so the complexity of this function will also be O(1) .
 
    bool containsValue(string value)
    {
        for (int i=0; i < hashSize;i++)
        {
            if(table[i]==NULL)
                continue;    
            if(table[i]->getValue()==value)
            {
                  return true;
            }
        }
        return false;
    }
      
**Smarter Hashtable:**

Smarter hashtable is implemented using chaining, by creating an array of linked list to store values  that were returning the same HashCode. The _insert()_ 
and _containValue()_ function will have the worst time complexity of O(n) due to LinkedList. To reduce the complexity, we can increase the size of LinkedList Array.
                
    void  insert(int key, string value)
    {
        bool allowInsertion = false;
        int hashIndex = hashFunction(key);

        //if list is empty just enter the data
        if(table[hashIndex].empty())
        {
            allowInsertion = true;
        }
        else
        {
            auto pointer = table[hashIndex].begin();
            allowInsertion = true;
            do
            {
                //if dublicate is found then replace the value of previous key
                if(pointer->getKey()==key)
                {
                    cout << "Duplicate key("<<key<<") found!"<<endl;
                    pointer->setValue(value);
                    allowInsertion = false;
                    break;
                }
                pointer++;
            } while (pointer != table[hashIndex].end());
        } 
        if(allowInsertion)
        {
            HashNode temp(key, value);
            table[hashIndex].push_back(temp);
        }
    }
 

    bool containsValue(string value)
    {
        for (int i=0; i < hashSize;i++)
        {
            if(table[i].empty())
                continue;
            auto pointer = table[i].begin();
            do
            {
                if(pointer->getValue()==value)
                {
                    return true;
                }
                pointer++;
            } while (pointer != table[i].end());
        }
        return false;
    } 
