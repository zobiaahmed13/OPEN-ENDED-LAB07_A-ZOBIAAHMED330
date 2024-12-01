# OPEN-ENDED-LAB07_A-ZOBIAAHMED330
//ZOBIA AHMED / 2022F-BSE-330 / LAB 07 / TASK 01:
package ZOBIA330LAB07TASK03;
import java.util.HashMap;
import java.util.Map;
public class ZOBIA330LAB07TASK03 {
	public static class BakeryInventory {
	    private Map<String, Product> products;
	    public BakeryInventory() {
	        products = new HashMap<>();
	    }
	    // Product class representing each bakery product
	    private class Product {
	        String name;
	        int stock;
	        public Product(String name, int stock) {
	            this.name = name;
	            this.stock = stock;
	        }
	    }
	    // Add a new product to the inventory
	    public void addProduct(String productId, String name, int initialStock) {
	        products.put(productId, new Product(name, initialStock));
	    }
	    // Update stock after a sale
	    public void recordSale(String productId, int quantity) {
	        if (products.containsKey(productId)) {
	            Product product = products.get(productId);
	            if (product.stock >= quantity) {
	                product.stock -= quantity;
	                System.out.println("Sold " + quantity + " of " + product.name);
	            } else {
	                System.out.println("Insufficient stock for " + product.name);
	            }
	        } else {
	            System.out.println("Product not found: " + productId);
	        }
	    }
	    // Get current stock level
	    public int getStockLevel(String productId) {
	        if (products.containsKey(productId)) {
	            return products.get(productId).stock;
	        }
	        System.out.println("Product not found: " + productId);
	        return 0; // or throw an exception
	    }
	    // Display all products in stock
	    public void displayStock() {
	        System.out.println("(*): Current Stock Levels:");
	        for (Map.Entry<String, Product> entry : products.entrySet()) {
	            System.out.println("Product ID: " + entry.getKey() + ", Name: " + entry.getValue().name + ", Stock: " + entry.getValue().stock);
	        }
	    }
	    public static void main(String[] args) {
	    	System.out.println("ZOBIA AHMED / 2022F-BSE-330 / LAB 07 / TASK 01:\n");
	    	System.out.println("(*): SCENERIO: BAKERY PRODUCT STOCK(BAKERY PRODUCT SELLING):");
	    	System.out.println("(*): OBJECTIVE: Implement Good Code Practices and Optimization Techniques:\n");
	        BakeryInventory inventory = new BakeryInventory();
	        inventory.addProduct("001", "CUP CAKES", 100);
	        inventory.addProduct("002", "BROWNIES", 100);
	        inventory.addProduct("003", "BISCUITS", 1000);
	        inventory.addProduct("004", "PIZZAS", 60);
	        inventory.addProduct("005", "DOUGHNUTS", 300);
	        inventory.addProduct("006", "LOAF BREADS", 200);
	        // Display total stock before selling
	        inventory.displayStock();
	        // Perform selling transactions
	        System.out.println("\n");
	        System.out.println("(*): TOTAL ITEMS SOLD TODAY:");
	        inventory.recordSale("001", 80);
	        inventory.recordSale("002", 75);
	        inventory.recordSale("003", 880);
	        inventory.recordSale("004", 35);
	        inventory.recordSale("005", 250);
	        inventory.recordSale("006", 175);
	        // Display remaining stock after selling
	        System.out.println("\n(*): Remaining Stock After Sales:");
	        inventory.displayStock();
	    }
	}
}

//ZOBIA AHMED / 2022F-BSE-330 / LAB 07 / TASK 02:
package ZOBIA330LAB07TASK04;
import java.util.HashMap;
import java.util.Map;
public class ZOBIA330LAB07TASK04 {
	// Main class managing the bakery inventory
	public static class BakeryInventory {
	    private Map<String, Product> products;
	    public BakeryInventory() {
	        products = new HashMap<>();
	    }
	    // Product class representing each bakery product
	    private class Product {
	        String name;
	        int stock;

	        public Product(String name, int stock) {
	            this.name = name;
	            this.stock = stock;
	        }
	    }
	    // Method to add a new product to the inventory
	    public void addProduct(String productId, String name, int initialStock) {
	        products.put(productId, new Product(name, initialStock));
	    }
	    // Method to simulate selling a product
	    public synchronized void recordSale(String productId, int quantity) {
	        if (products.containsKey(productId)) {
	            Product product = products.get(productId);
	            if (product.stock >= quantity) {
	                product.stock -= quantity;
	                System.out.println(Thread.currentThread().getName() + ": Sold '" + quantity + "' " + product.name);
	            } else {
	                System.out.println(Thread.currentThread().getName() + ": Insufficient stock for " + product.name);
	            }
	        } else {
	            System.out.println(Thread.currentThread().getName() + ": Product not found: " + productId);
	        }
	    }
	    // Method to display current stock levels
	    public void displayStock() {
	        System.out.println("\n(*): Current Stock Levels:");
	        for (Map.Entry<String, Product> entry : products.entrySet()) {
	            System.out.println("Product ID: " + entry.getKey() + ", Name: " + entry.getValue().name + ", Stock: " + entry.getValue().stock);
	        }
	    }
	    // Thread for handling sales
	    private class SalesThread extends Thread {
	        private String productId;
	        private int quantity;

	        public SalesThread(String productId, int quantity) {
	            this.productId = productId;
	            this.quantity = quantity;
	        }
	        @Override
	        public void run() {
	            try {
	                // Simulate processing time
	                Thread.sleep(1000); // Sleep for 1 second
	                recordSale(productId, quantity);
	            } catch (InterruptedException e) {
	                System.out.println(Thread.currentThread().getName() + " was interrupted.");
	            }
	        }
	    }
	    // Thread for logging stock levels
	    private class LogThread extends Thread {
	        @Override
	        public void run() {
	            try {
	                // Simulate logging delay
	                Thread.sleep(500); // Sleep for 0.5 seconds
	                displayStock();
	            } catch (InterruptedException e) {
	                System.out.println(Thread.currentThread().getName() + " was interrupted.");
	            }
	        }
	    }
	    public static void main(String[] args) {
	    	System.out.println("ZOBIA AHMED / 2022F-BSE-330 / LAB 07 / TASK 02:\n");
	    	System.out.println("(*): SCENERIO: BAKERY PRODUCT STOCK(BAKERY PRODUCT SELLING):");
	    	System.out.println("(*): OBJECTIVE: Concurrency with Multithreading Mechanisms:");
	        BakeryInventory inventory = new BakeryInventory();
	        inventory.addProduct("001", "CUP CAKES", 100);
	        inventory.addProduct("002", "BROWNIES", 100);
	        inventory.addProduct("003", "BISCUITS", 1000);
	        inventory.addProduct("004", "PIZZAS", 60);
	        inventory.addProduct("005", "DOUGHNUTS", 300);
	        inventory.addProduct("006", "LOAF BREADS", 200);
	        // Display total stock before selling
	        inventory.displayStock();
	        // Perform selling transactions:
	        // Create threads for sales and logging:
	        System.out.println("");
	        System.out.println("(*): TOTAL ITEMS SOLD TODAY:");
	        SalesThread salesThread1 = inventory.new SalesThread("001", 5);
	        SalesThread salesThread2 = inventory.new SalesThread("002", 10);
	        LogThread logThread = inventory.new LogThread();
	        // Start sales threads
	        salesThread1.start();
	        salesThread2.start();
	        try {
	            // Ensure that sales threads complete before logging
	            salesThread1.join(); // Wait for salesThread1 to finish
	            salesThread2.join(); // Wait for salesThread2 to finish
	        } catch (InterruptedException e) {
	            System.out.println("Main thread was interrupted.");
	        }
	        // Start logging thread after sales are complete
	        logThread.start();
	        try {
	            // Wait for logging thread to complete
	            logThread.join(); // Ensure logThread completes before exiting main
	        } catch (InterruptedException e) {
	            System.out.println("Main thread was interrupted.");
	        }
	    }
	}
}

//ZOBIA AHMED / 2022F-BSE-330 / LAB 07 / TASK 05:
package ZOBIA330LAB07TASK05;
import java.util.LinkedList;
import java.util.Queue;
public class ZOBIA330LAB07TASK05 {
	public static class BakeryInventory {
	    private final Queue<String> stockBuffer;
	    private final int capacity;
	    public BakeryInventory(int capacity) {
	        this.capacity = capacity;
	        this.stockBuffer = new LinkedList<>();
	    }
	    // Producer class that adds products to the buffer
	    private class Producer extends Thread {
	        private final String product;
	        public Producer(String product) {
	            this.product = product;
	        }

	        @Override
	        public void run() {
	            try {
	                while (true) {
	                    produce(product);
	                    Thread.sleep(10); // Simulate time taken to produce
	                }
	            } catch (InterruptedException e) {
	                Thread.currentThread().interrupt();
	            }
	        }
	        private synchronized void produce(String product) throws InterruptedException {
	            while (stockBuffer.size() == capacity) {
	                System.out.println("Buffer is full. Producer is waiting.");
	                wait(); // Wait until space is available
	            }
	            stockBuffer.add(product);
	            System.out.println("Produced: " + product);
	            notify(); // Notify a waiting consumer
	        }
	    }
	    // Consumer class that removes products from the buffer
	    private class Consumer extends Thread {
	        @Override
	        public void run() {
	            try {
	                while (true) {
	                    consume();
	                    Thread.sleep(10); // Simulate time taken to consume
	                }
	            } catch (InterruptedException e) {
	                Thread.currentThread().interrupt();
	            }
	        }
	        private synchronized void consume() throws InterruptedException {
	            while (stockBuffer.isEmpty()) {
	                System.out.println("Buffer is empty. Consumer is waiting.");
	                wait(); // Wait until items are available
	            }
	            String product = stockBuffer.poll();
	            System.out.println("Consumed: " + product);
	            notify(); // Notify a waiting producer
	        }
	    }
	    public static void main(String[] args) {
	        BakeryInventory inventory = new BakeryInventory(5); // Buffer capacity of 5
	        System.out.println("ZOBIA AHMED / 2022F-BSE-330 / LAB 07 / TASK 05:\n");
	    	System.out.println("(*): SCENERIO: BAKERY PRODUCT STOCK(BAKERY PRODUCT SELLING):");
	    	System.out.println("(*): OBJECTIVE: Inter-Thread Communication Using Synchronization:");
	        // Create producer and consumer threads
	        Producer producer1 = inventory.new Producer("CUP CAKES");
	        Producer producer2 = inventory.new Producer("BROWNIES");
	        Producer producer3 = inventory.new Producer("BISCUITS");
	        Producer producer4 = inventory.new Producer("LOAF BREADS");
	        Consumer consumer = inventory.new Consumer();
	        // Start the threads
	        producer1.start();
	        producer2.start();
	        producer3.start();
	        producer4.start();
	        consumer.start();
	    }
	}
}
