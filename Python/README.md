[Go back](./../README.md)

## Contents
* [Numpy](./Numpy%20Notes.txt)
* [Pandas](./Pandas%20Notes.txt)
* [Dump and Load Pickle](#dump-and-load-pickle)
* [Networkx](#network-x)
* [OOPS](#oops)

---

## Dump and Load Pickle

One line functions for load and dump pickle file
> NOTE: Make sure to `import pickle`

```python
def load_pkl(path,pickle_alis=False):
    pk = pickle_alis if pickle_alis else pickle
    file = open(path,"br")
    item = pk.load(file)
    file.close()
    return item
    
def dump_pkl(item,path,pickle_alis=False):
    pk = pickle_alis if pickle_alis else pickle
    file = open(path,"bw")
    pk.dump(item,file)
    file.close()
```

---

## Network X

We can add any python object(dict,str,list...) to the node of graph even a *graph itself.*

#### Graph Creation 
```python
G = nx.Graph() # Undirected Graph
or
G = nx.DiGraph() #Directed Graph
```

#### Methods

|Method|Description|
|:-:|:-|
|`G.add_node([object])`|Add a Node to the Graph|
|`G.add_nodes_from(param)`|This method allows us to add multiple nodes at a time to the graph.`@param=list`|
|`G.add_edge(param)`|Connect the nodes.`@param=tuple *(from,to)*`<br>This command connect the create node if the inputs are not in the Graph.|
|`G.add_edges_from(param)`|We can pass a list of tuples to connect their nodes.`@param=list(tuple)`|
|`G.add_weighted_edges_from(param)`|We can connect the edges with the weight values.<br>`G.add_weighted_edges_from([(from,to,[object]),...])`|

> For a Directed graph we have to add the edges in the format as [from,to] and [to,from]

#### Diffrent ways of Adding nodes and Edges

|||
|:-:|:-|
|`G.add_nodes_from([(node_name,node_data),...])`<br>`G.add_nodes_from([nodes],default_name=default_node_data)`|Here the `default_name` will set to the each node if data is already present before this new will replace it|

### Assign the values
We can assign the values for nodes by following the similar process for *dictionary*.
```python
for i in G.nodes:   #G.nodes -> returns the Iterable nodes
    G.nodes[i]['male'] = True
    G.nodes[i]['age'] = np.random.choice(range(10,80))
```

### Access the values
```python
G.nodes[node_name] #returns the node data
G.edges[from_node,to_node] #returns the edge weight between nodes
```

|Method|Description|
|:-:|:-|
|`G.degree()`|Returns the degree of the nodes in form a `dict`|
|`G.adj`|Returns a `dict` with data containing the neighbors of each node and the edge value to it|
|`G.neighbors(node_name)`|Return the Iterable Neighbors of the node|
|`G.nodes.data()`|Return the Complete node data of the all nodes in the `dict`|


### Plot the Graph

```python
plt.figure(1)
nx.draw_networkx(G,with_labels=True,arrows=True)
plt.show()
#YOu can also give node_color=[len(nodes)*<colors>] to represent each node with color
#                  node_size=[len(nodes)*sizes] to represent diffrent sizes for each node
```

---

## OOPS

```python
class ClassName:
    def __init__(self): # constructor
        ...
    
    def methods(self):
        ...
```

List of concepts are

### Encapsulation
Use the class without knowing how it is build
```python
object = ClassName()
object.methods()
```
### Inheritance
Inherit the parent class. if the child doesn't have a constructor the default constructor is parent one.
```python
class Child(Parent):
    ...
```
> we can access parent constructor using **super()**.

### Polymorphism
Modify the parent class methods 
```python
class Parent:
    ...
    def parentmethod(self):
        pass

class Child(Parent):
    ...
    def paerntmethod(self):
        ...
```

### Abstraction
Must and should layout build for classes that inherits it 
```python
from abc import ABCMeta, abstractmethod

# This class cannot be instantiated
class BaseClass(metaclass=ABCMeta):
    
    #constructor not mandatory

    @abstractmethod
    def method_name(self):
        pass

class DerivedClass(BaseClass):
    def __init__(self):
        pass

    # Should have the method
    def method_name(self):
        ...

```