

## Representation of Graph

1. [Directed Weighted Graph](https://tutorialhorizon.com/algorithms/weighted-graph-implementation-java/)


```java
import java.util.LinkedList;

class Scratch {
    public static void main(String[] args) {
        // n = 3, edges = [[0,1],[1,2],[0,2]], succProb = [0.5,0.5,0.3], start = 0, end = 2
        Graph g = new Graph(3);
        g.addEgde(0, 1, 0.5);
        g.addEgde(1, 2, 0.5);
        g.addEgde(0, 2, 0.3);
        g.printGraph();
    }
    static class Edge {
        int source;
        int destination;
        double weight;

        public Edge(int source, int destination, double weight) {
            this.source = source;
            this.destination = destination;
            this.weight = weight;
        }
    }

    static class Graph {
        int vertices;
        LinkedList<Edge>[] adjacencylist;

        Graph(int vertices) {
            this.vertices = vertices;
            adjacencylist = new LinkedList[vertices];

            //initialize adjacency lists for all the vertices
            for (int i = 0; i <vertices ; i++) {
                adjacencylist[i] = new LinkedList<>();
            }
        }

        public void addEgde(int source, int destination, double weight) {
            Edge edge = new Edge(source, destination, weight);
            Edge reverseEdge = new Edge(destination, source, weight);
            adjacencylist[source].add(edge);
            adjacencylist[destination].add(reverseEdge);
        }
        public void printGraph(){
            for (int i = 0; i <vertices ; i++) {
                LinkedList<Edge> list = adjacencylist[i];
                for (int j = 0; j <list.size() ; j++) {
                    System.out.println("vertex-" + i + " is connected to " +
                            list.get(j).destination + " with weight " +  list.get(j).weight);
                }
            }
        }
    }
}
```

#### output
```
vertex-0 is connected to 1 with weight 0.5
vertex-0 is connected to 2 with weight 0.3
vertex-1 is connected to 0 with weight 0.5
vertex-1 is connected to 2 with weight 0.5
vertex-2 is connected to 1 with weight 0.5
vertex-2 is connected to 0 with weight 0.3
```
