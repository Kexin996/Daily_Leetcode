# Untitled



```
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) 
    {
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        if (edges.length == 0)
        {
            List<Integer> ans = new ArrayList<Integer>();
            ans.add(0);
            return ans;
        }
        for (int i = 0; i < n; i++)
        {
            adj.add(new ArrayList<Integer>());
        }
```

```
    for (int[] set: edges)
    {
        adj.get(set[0]).add(set[1]);
        adj.get(set[1]).add(set[0]);

    }
    // Queue implemantation
    Queue<Integer> leaves = new LinkedList<Integer>();
    for (int i = 0; i < n; i++)
    {
        if (adj.get(i).size() == 1)
        {
            leaves.add(i);
        }
    }
    while (n > 2)
    {
        // why we cannot use the leaves.size() as iterator
        // if the number of leaves == 2, the whole while-loop
        // will not be executed
        int temp = leaves.size();
        n-=temp;
        while (temp-- > 0)
        {
            int temp1 = leaves.poll();
            for (int i = 0; i < adj.get(temp1).size();i++)
            {
                int val = adj.get(temp1).get(i);
                adj.get(val).remove(adj.get(val).indexOf(temp1));
                if (adj.get(val).size() == 1)
                {
                    leaves.add(val);
                }
            }
        }
    }
    return (List)leaves;
    
    /*
    List<Integer> leaves = new LinkedList<Integer>();
    for (int i = 0; i < n;i++)
    {
        if (adj.get(i).size() == 1)
        {
            leaves.add(i);
        }
    }
    while (n > 2)
    {
        List<Integer> newLeaves = new LinkedList<Integer>();
        n -= leaves.size();
        for (int i: leaves)
        {
            List<Integer> val = adj.get(i);
            for (int j: val)
            {
                adj.get(j).remove(adj.get(j).indexOf(i));
                if (adj.get(j).size() == 1)
                {
                    newLeaves.add(j);
                }
            }
        }
        leaves = newLeaves;
    }
    return leaves;
    */
}
```

}
