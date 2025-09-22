# 133. Clone Graph
https://leetcode.com/problems/clone-graph/description/?envType=problem-list-v2&envId=oizxjoit

## Code
```cpp
Node* cloneGraph(Node* node) {
    unordered_map<Node*, Node*> map;

    if ( node == nullptr )
    {
        return nullptr;
    }

    if ( node->neighbors.size() == 0 )
    {
        return new Node( node->val );
    }

    return dfsCopy( node, map );
}

Node* dfsCopy( Node* cur, unordered_map<Node*, Node*>& map )
{
    vector<Node*> neighbors;

    Node* clone = new Node( cur->val );

    map[ cur ] = clone;

    for ( Node* neighbor : cur->neighbors )
    {
        if ( map.find( neighbor ) != map.end() )
        {
            neighbors.push_back( map[ neighbor ] );
        }
        else
        {
            neighbors.push_back( dfsCopy(neighbor, map ));
        }
    }

    clone->neighbors = neighbors;

    return clone;
}
```

## Basic idea
DFS. Maintain a map of visited nodes and their clone. Iterate over a nodes neighbors, if its neighbor has a clone (i.e. has been visited) we add the clone, otherwise we add the result of DFS on that neighbor. Return the result of DFS on the head of the graph.

## Time complexity
We check every node and edge once, so our time complexity is $O(V + E)$, same as DFS (assuming $O(1)$ `unordered_map` lookup).