import java.util.*;

class Product {
    int id, quantity;
    String name;
    double price;
    Product(int id, String name, int quantity, double price) {
        this.id = id; this.name = name; this.quantity = quantity; this.price = price;
    }
    public String toString() { return id + " | " + name + " | Qty: " + quantity + " | Price: " + price; }
}

class Inventory {
    ArrayList<Product> products = new ArrayList<>();
    void add(Product p) { products.add(p); System.out.println("Product added!"); }
    void view() {
        if(products.isEmpty()) System.out.println("Inventory is empty!");
        else products.forEach(System.out::println);
    }
    void search(int id) {
        for(Product p: products) if(p.id==id){System.out.println("Found: "+p); return;}
        System.out.println("Not found!");
    }
    void delete(int id) {
        if(products.removeIf(p -> p.id==id)) System.out.println("Product deleted!");
        else System.out.println("Not found!");
    }
}

public class Main1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Inventory inv = new Inventory();
        while(true){
            System.out.println("\n--- Inventory Management System ---");
            System.out.println("1. Add Product");
            System.out.println("2. View Products");
            System.out.println("3. Search Product");
            System.out.println("4. Delete Product");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");
            switch(sc.nextInt()){
                case 1 -> {
                    System.out.print("ID: "); int id = sc.nextInt();
                    System.out.print("Name: "); String name = sc.next();
                    System.out.print("Quantity: "); int qty = sc.nextInt();
                    System.out.print("Price: "); double price = sc.nextDouble();
                    inv.add(new Product(id,name,qty,price));
                }
                case 2 -> inv.view();
                case 3 -> { System.out.print("ID to search: "); inv.search(sc.nextInt()); }
                case 4 -> { System.out.print("ID to delete: "); inv.delete(sc.nextInt()); }
                case 5 -> { sc.close(); return; }
                default -> System.out.println("Invalid choice!");
            }
        }
    }
}
