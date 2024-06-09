// Node.java


public class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

// SinglyLinkedList.java


public class SinglyLinkedList {
    private Node head;

    public SinglyLinkedList() {
        this.head = null;
    }

    // Metoda do dodawania nowego elementu na początku listy
    public void addFirst(int data) {
        Node newNode = new Node(data);
        newNode.next = head;
        head = newNode;
    }

    // Metoda do dodawania nowego elementu na końcu listy
    public void addLast(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }

    // Metoda do usuwania elementu z początku listy
    public void removeFirst() {
        if (head != null) {
            head = head.next;
        }
    }

    // Metoda do usuwania elementu z końca listy
    public void removeLast() {
        if (head == null) {
            return;
        }
        if (head.next == null) {
            head = null;
            return;
        }
        Node current = head;
        while (current.next.next != null) {
            current = current.next;
        }
        current.next = null;
    }

    // Metoda do wyświetlania wszystkich elementów listy
    public void display() {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        SinglyLinkedList list = new SinglyLinkedList();
        list.addFirst(1);
        list.addLast(2);
        list.addLast(3);
        list.addFirst(0);

        list.display(); // Output: 0 -> 1 -> 2 -> 3 -> null

        list.removeFirst();
        list.display(); // Output: 1 -> 2 -> 3 -> null

        list.removeLast();
        list.display(); // Output: 1 -> 2 -> null
    }                
}
