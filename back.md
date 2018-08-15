B
ehavior Questions
Self Introduction
who you are? My name is Yifan Jiang and I just received my Master degree from Texas A&M University this May. I'm currently seeking a new graduate software engineer position starting from any time.

Expertise Highlights I have spent years developing my skills as a software engineer. From all my coursework and projects, I acquire diverse skills include software development and web application design.

Team work I really love teamwork especially for challenging projects. In my lastest full-stack Scrum project, I worked as the Scrum master to make detailed plans for each iteration, motive the whole team and communicate with clients and customers. When we encounter some difficulties, we work harder and harder to solve the problem together. It makes me feel so happy to have a nice team sharing your work and make progress together.

Why You’re Here I love technology and willing to keep learning latest technology and embrace many difficult challenges with great ambition to benefit lives with cutting-edge technology.

Resume Projects
Full Stack Scrum Development For SaaS Application

I think it's the most difficult project because our team build this web application from scratch while interacting with our customers.
In iteration 0, we did a lot of preparation for our coming work including creating user stories and designing UI sample.
Then based on MVC model, I designed different data models for different users and their corresponding relationship. Then wrote controllers for each data model and corresponding views with CSS/Bootstrap(beautify buttons and background frames, the navigation bar, the responsive web) and using JavaScript for some interactive experience(insert a small application like calendar or send messages from each other).
Test is also an important part, first do cucumber test, which is on behavior level, then do RSpec test which is on specific function level. All our development use Git to control version and deployed to Heroku after each iteration.
Keep in touch with customers because customers' need always change and we have to catch up with their latest requirements and modify our application. I really learned a lot from back end to front end during this project.
Network Routing Optimization

This is a project that apply many data structures and algorithms using Java.
In order to study the different algorithm efficiency in network routing, I first generate two graph models to simulate the real-world complex networks with Java, one is sparse graph with few connections among each other(light/green network with few users like in the morning), the other is dense graph with a lot of connections among each other(heavy network with a lot of users, like holidays).
There are usually two ways to generate a graph, one is Linked list and the other is Adjacency Matrix. However, when the graph is dense, it's even better to use bitmap to save huge space.
Each graph node represents a router or gateway in real network, we need to find the maximum bandwidth path between source and destination. The maximum bandwidth from source to destination equals the minimum bandwidth on each edge, this is the bottleneck for the bandwidth. Our job is finding the path which has the max minimum bandwidth.
We apply different algorithms like Dijkstra, Kruskal and different data structures like linked list and heap(as for heap, each insertion and deletion takes extra steps, but it's really easy to get the maximum and minimum which is on the top or heap, but for each insertion and deletion, need to adjust its position to make this heap correct again).
Dijkstra's algorithm: find the shortest path between a and b. It picks the unvisited vertex with the lowest distance, calculates the distance through it to each unvisited neighbor, and updates the neighbor's distance if smaller. Mark visited when done with neighbors.
Kruskal: minimum spanning tree, sort the edges from small to large, then add edges to the graph, when reach the minimum spanning tree, then it's optimal
Socket Programming and NS-2 Simulation

I/O multiplexing handle sending and receiving messages at the same time.
Trivial File Transfer Protocol (TFTP) is a simple FTP which allows a client to get from or put a file onto a remote host. TFTP has been used for this application because it is very simple to implement.
Http proxy: it has limit like 10 files space, when it download from server, it just store the file in local place as cache, if the client ask for the same file, the proxy send it to the client directly without downloading from the server again. Once local files is out of space limit, it will delete the least active or used files. In this way, it's very efficient to handle the repeated request for the same file.
Genetic-Based Machine Learning Approaches

We want to know from a huge amount of data, use maching learning method to find a classifier to identify gene-expression signature.
Given a gene dataset, there is a training dataset which is used for customizing specific classifier and a test dataset which is used for calculating the error rate as the criteria for our classifier.
Implemented LDA, KNN and SVM algorithms to customizing classifier.
The whole performance based on classifier design, error estimation, and feature selection techniques
Then use parallel computing approach to accelerate, computer usually has multiple cores, we can split the work into different cores. However, there is one thing, that is allocating work to different cores also could slow down the performance. So try to allocate more cores to accelerate.
Database and Interactive User Interface Design

there is a need to create a specific database for customers. We design the data models and their relationship between each other using MYSQL. Then generate a large number of random test data and input into our new database.
Then we need to build a simple application to help our customers to use this database directly. Using Java, we first connect to the MYSQL server and ask for the right to connect to our newly created database.
After having access to the database, we build a simple application continuously getting the customers request with CRUD method and keywords for the data we need to access. Then collecting data and do analysis on it.
Dijkstra
import java.util.*;
public class Test {
    public static void main(String[] args) {
        Test t = new Test();
        List<GraphNode> graph = t.buildGraph();
        System.out.println(t.Dijkstra(graph,graph.get(0),graph.get(8)));

    }
    public int Dijkstra(List<GraphNode> graph, GraphNode start, GraphNode end){
        int[] status = new int[graph.size()];
        Arrays.fill(status,-1);
        PriorityQueue<GraphNode> heap = new PriorityQueue<>(new Comparator<GraphNode>(){
            public int compare(GraphNode n1, GraphNode n2){
                return n2.max_bandwith - n1.max_bandwith;
            }
        });
        status[start.node] = 1;//in-tree
        for(Edge each : start.next){
            status[each.to.node] = 0;
            each.to.max_bandwith = each.weight;
            heap.offer(each.to);
        }
        while(status[end.node] != 1 ){//while end not in-tree
            GraphNode crt = heap.poll();
            // System.out.println(crt.node);
            status[crt.node] = 1;
            for(Edge each : crt.next){
                if(status[each.to.node] == -1){
                    status[each.to.node] = 0;
                    each.to.max_bandwith = Math.min(crt.max_bandwith,each.weight);
                    heap.offer(each.to);
                }else if(status[each.to.node] == 0 && each.to.max_bandwith < Math.min(crt.max_bandwith,each.weight)){
                    each.to.max_bandwith = Math.max(each.to.max_bandwith, Math.min(crt.max_bandwith,each.weight));
                    heap.remove(each.to);
                    heap.offer(each.to);
                }
            }
        }
        return end.max_bandwith;
    }
    public List<GraphNode> buildGraph(){
        List<GraphNode> rst = new ArrayList<>();
        for(int i=0;i<9;i++) rst.add(new GraphNode(i,0));
        rst.get(0).next.add(new Edge(5,rst.get(0),rst.get(2)));
        rst.get(0).next.add(new Edge(4,rst.get(0),rst.get(1)));
        rst.get(1).next.add(new Edge(5,rst.get(1),rst.get(4)));
        rst.get(2).next.add(new Edge(4,rst.get(2),rst.get(5)));
        rst.get(2).next.add(new Edge(4,rst.get(2),rst.get(3)));
        rst.get(3).next.add(new Edge(8,rst.get(3),rst.get(4)));
        rst.get(4).next.add(new Edge(3,rst.get(4),rst.get(7)));
        rst.get(5).next.add(new Edge(4,rst.get(5),rst.get(6)));
        rst.get(6).next.add(new Edge(4,rst.get(6),rst.get(7)));
        rst.get(7).next.add(new Edge(5,rst.get(7),rst.get(8)));
        return rst;
    }
    public class GraphNode {
        int node;
        int max_bandwith;
        List<Edge> next;
        public GraphNode(int node, int max_bandwith){
            this.node = node;
            this.max_bandwith = max_bandwith;
            next = new ArrayList<>();
        }
    }
    public class Edge {
        int weight;
        GraphNode from,to;
        public Edge(int weight, GraphNode from, GraphNode to){
            this.weight = weight;
            this.from = from;
            this.to = to;
        }
    }
}
Kruskal’s algorithm (MST)
import java.util.*;
public class Test {
    public static void main(String[] args) {
        Test t = new Test();
        List<GraphNode> graph = t.buildGraph();
        System.out.println(t.Kruskal(graph,graph.get(0),graph.get(8)));

    }
    public int Kruskal(List<GraphNode> graph, GraphNode start, GraphNode end){
        List<Edge> edges = new ArrayList<>();
        for(GraphNode node : graph){
            for(Edge edge : node.next) edges.add(edge);
        }
        Collections.sort(edges, new Comparator<Edge>(){
            public int compare(Edge e1, Edge e2){
                return e2.weight - e1.weight;
            }
        });
        int max_bandwidth = Integer.MAX_VALUE;
        for(Edge edge : edges){
            GraphNode node1 = edge.from;
            GraphNode node2 = edge.to;
            if(getRoot(node1) == getRoot(node2)) return max_bandwidth;
            else {
                union(node1,node2);
                max_bandwidth = Math.min(max_bandwidth,edge.weight);
            }
        }
        return max_bandwidth;
    }
    public GraphNode getRoot(GraphNode node){
        while(node.root != node){
            node.root = node.root.root;
            node = node.root;
        }
        return node;
    }
    public void union(GraphNode node1, GraphNode node2){
        GraphNode root1 = getRoot(node1);
        GraphNode root2 = getRoot(node2);
        root1.root = root2;
    }
    public List<GraphNode> buildGraph(){
        List<GraphNode> rst = new ArrayList<>();
        for(int i=0;i<9;i++) rst.add(new GraphNode(i));
        rst.get(0).next.add(new Edge(5,rst.get(0),rst.get(2)));
        rst.get(0).next.add(new Edge(4,rst.get(0),rst.get(1)));
        rst.get(1).next.add(new Edge(5,rst.get(1),rst.get(4)));
        rst.get(2).next.add(new Edge(4,rst.get(2),rst.get(5)));
        rst.get(2).next.add(new Edge(4,rst.get(2),rst.get(3)));
        rst.get(3).next.add(new Edge(8,rst.get(3),rst.get(4)));
        rst.get(4).next.add(new Edge(3,rst.get(4),rst.get(7)));
        rst.get(5).next.add(new Edge(4,rst.get(5),rst.get(6)));
        rst.get(6).next.add(new Edge(4,rst.get(6),rst.get(7)));
        rst.get(7).next.add(new Edge(5,rst.get(7),rst.get(8)));
        return rst;
    }
    public class GraphNode {
        int node;
        GraphNode root;
        List<Edge> next;
        public GraphNode(int node){
            this.node = node;
            this.root = this;
            next = new ArrayList<>();
        }
    }
    public class Edge {
        int weight;
        GraphNode from,to;
        public Edge(int weight, GraphNode from, GraphNode to){
            this.weight = weight;
            this.from = from;
            this.to = to;
        }
    }
}
