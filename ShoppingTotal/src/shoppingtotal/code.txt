package shoppingtotal;

class PriceCalculator extends Thread {
    private int[] prices;
    private int total = 0;

    public PriceCalculator(int[] prices) {
        this.prices = prices;
    }

    public void run() {
        for (int price : prices) {
            total += price;
        }
    }

    public int getTotal() {
        return total;
    }
}

public class ShoppingTotal {
    public static void main(String[] args) {
        int[] group1 = {2000};  // Lashes, Eyeliner, Phone Cover
        int[] group2 = {1500};  // Lens
        int[] group3 = {8000};  // Cleaning Balm, Sunscreen, Toner, Moisturizer, Serum

        PriceCalculator t1 = new PriceCalculator(group1);
        PriceCalculator t2 = new PriceCalculator(group2);
        PriceCalculator t3 = new PriceCalculator(group3);

        t1.start();
        t2.start();
        t3.start();

        try {
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            System.out.println("Thread interrupted: " + e.getMessage());
        }

        int totalSum = t1.getTotal() + t2.getTotal() + t3.getTotal();
        System.out.println("Total Shopping Cost: " + totalSum + " BDT\n");

        // Print Valentine's Day message
        System.out.println("Happy Valentine's Day! \u2764");
    }
}
