# Week-10b
Tugas Artificial Intelligent and Aplication Week 10

Nama		: Almas Diqya Wafa’ 
NIM		: 5311421005
Prodi		: Teknik Elektro
Mata Kuliah	: Artificial Intellegent and Aplication
Rombel	: Senin 09.00

MODUL 4
“Teknik Pencarian Blind Search”

2.	Ubahlah method static void main sehingga bentuk tree seperti Gambar 4.5 dapat dibentuk. Kemudian tentukan bagaimana algoritma BFS dapat menemukan node 5.
Program:
import java.util.ArrayDeque; 
import java.util.ArrayList; 
import java.util.HashMap; 
import java.util.List; 
import java.util.Map; 
import java.util.Queue; 
import java.util.Set; 

public class AdjacencyList 
{ 
public enum NodeColour { WHITE, GRAY, BLACK } 
public static class Node 
{ 
int data; 
int distance; 
NodeColour colour; 
public Node(int data) 
{ 
            this.data = data; 
        } 
        
    /**
     *
     * @return
     */
    @Override
        public String toString() 
        { 
         return "(" + data + ",d=" + distance + ")"; 
        } 
    } 
    
    Map<Node, List<Node>> nodes; 
 
    public AdjacencyList() 
    { 
        nodes = new HashMap<>(); 
    } 
    
    public void addEdge(Node n1, Node n2) 
    { 
        if (nodes.containsKey(n1)) { 
            nodes.get(n1).add(n2); 
        } else { 
       ArrayList<Node> list = new ArrayList<>(); 
            list.add(n2); 
            nodes.put(n1, list); 
        } 
    } 
    
    public void bfs(Node s) 
    { 
        Set<Node> keys = nodes.keySet(); 
        for (Node u : keys) { 
            if (u != s) { 
                u.colour = NodeColour.WHITE; 
                u.distance = Integer.MAX_VALUE; 
            } 
        } 
        s.colour = NodeColour.GRAY; 
        s.distance = 0; 
        Queue<Node> q = new ArrayDeque<>(); 
        q.add(s); 
        while (!q.isEmpty()) { 
            Node u = q.remove(); 
            List<Node> adj_u = nodes.get(u); 
            if (adj_u != null) { 
                for (Node v : adj_u) { 
                    if(v.colour == NodeColour.WHITE) { 
                        v.colour = NodeColour.GRAY; 
                        v.distance = u.distance + 1; 
                        q.add(v); 
                    } 
                } 
            } 
            u.colour = NodeColour.BLACK; 
            System.out.print(u + " "); 
        } 
    } 
    public static void main(String[] args) { 
    AdjacencyList graph = new AdjacencyList(); 
    Node n0 = new Node(0); 
    Node n1 = new Node(1); 
    Node n2 = new Node(2); 
    Node n3 = new Node(3); 
    Node n4 = new Node(4); 
    Node n5 = new Node(5); 
    Node n6 = new Node(6); 
    
    graph.addEdge(n0, n1); 
    graph.addEdge(n0, n2); 
    graph.addEdge(n1, n0); 
    graph.addEdge(n1, n3); 
    graph.addEdge(n1, n4); 
    graph.addEdge(n2, n0); 
    graph.addEdge(n2, n5); 
    graph.addEdge(n2, n6); 
    graph.addEdge(n3, n1); 
    graph.addEdge(n3, n4);
    graph.addEdge(n4, n3); 
    graph.addEdge(n4, n1);
    graph.addEdge(n5, n2); 
    graph.addEdge(n5, n6);
    graph.addEdge(n5, n1); 
    graph.addEdge(n6, n2);
    graph.addEdge(n6, n5); 
    graph.addEdge(n6, n1);
    
    
    graph.bfs(n0); 
    }
}

Hasil:
Setelah melakukan praktikum menggunakan software Netbeans dan melakukan uji coba pada Modul 4 (nomor 2) ditemukan hasil sebagai berikut.
(0,d=0) (1,d=1) (2,d=1) (3,d=2) (4,d=2) (5,d=2) (6,d=2) BUILD SUCCESSFUL (total time: 0 seconds)

Penjelasan:
Untuk mengubah metode main agar menciptakan pohon seperti yang diinginkan dalam Gambar 4.5, kita harus mengubah program pada metode main seperti di atas. Dalam perubahan ini, simpul-simpul dan tepi-tepi yang ditambahkan sesuai dengan Gambar 4.5. Simpul 0 memiliki dua anak, yaitu 1 dan 2. Simpul 1 memiliki dua anak, yaitu 3 dan 4. Simpul 2 memiliki dua anak, yaitu 5 dan 6.

Untuk menjelaskan bagaimana algoritma BFS menemukan node 5, berikut adalah langkah-langkahnya:

1. *Node 0 (d=0):* BFS dimulai dari simpul n0 dengan jarak 0.
2. *Node 1 (d=1):* n0 memiliki dua anak, n1 dan n2. BFS melanjutkan ke n1 dengan jarak 1.
3. *Node 3 (d=2):* n1 memiliki dua anak, n3 dan n4. BFS melanjutkan ke n3 dengan jarak 2.
4. *Node 4 (d=2):* n1 juga memiliki anak n4, tetapi n4 sudah diwarnai GRAY (dalam proses BFS), jadi BFS tidak melanjutkan ke n4.
5. *Node 2 (d=1):* Setelah menyelesaikan anak-anak n1, BFS kembali ke n0 dan melanjutkan ke n2 dengan jarak 1.
6. *Node 5 (d=2):* n2 memiliki anak n5. BFS melanjutkan ke n5 dengan jarak 2.

Dengan demikian, algoritma BFS pada graf di atas menemukan node 5 dengan jarak 2 dari node awal (n0).

