namespace ConsoleApp2
{
    internal class Program
    {
        static void Main(string[] args)
        {
            string[,] products = new string[5, 4];

            Console.WriteLine("Let's enter some product details. You can add 5 products.");

            for (int dj = 0; dj < 5; dj++)
            {
                Console.WriteLine($"Let's add details for product {dj + 1}:");

                Console.Write("What is the name of the product? ");
                products[dj, 0] = Console.ReadLine();

                Console.Write("What category does the product belong to? ");
                products[dj, 1] = Console.ReadLine();

                double price;
                Console.Write("Enter the price: ");
                while (!double.TryParse(Console.ReadLine(), out price))
                {
                    Console.Write("Oops! Can you try again? ");
                }
                products[dj, 2] = price.ToString();

                int quantity;
                Console.Write("How many of these are in stock? ");
                while (!int.TryParse(Console.ReadLine(), out quantity))
                {
                    Console.Write("Hmm, that does not look like a number. Can you try again? ");
                }
                products[dj, 3] = quantity.ToString();

                Console.WriteLine("Great! Let's move on to the next product.");
            }

            DisplayProductDetails(products);
            CalculateTotalStockValue(products);

            Console.WriteLine("\nThank you for providing the product details!");
        }

        static void DisplayProductDetails(string[,] products)
        {
            Console.WriteLine("\nHere are the products you've entered:");
            Console.WriteLine("\nProduct Name | Category   | Price  | Quantity");

            foreach (var i in Enumerable.Range(0, products.GetLength(0)))
            {
                Console.WriteLine($"{products[i, 0]} | {products[i, 1]} | ${products[i, 2]} | {products[i, 3]} units");
            }
        }

        static void CalculateTotalStockValue(string[,] products)
        {
            Console.WriteLine("\nNow, let's see the total stock value for each product");
            Console.WriteLine("Product Name | Total Stock Value");

            foreach (var i in Enumerable.Range(0, products.GetLength(0)))
            {
                double price = Convert.ToDouble(products[i, 2]);
                int quantity = Convert.ToInt32(products[i, 3]);
                double totalValue = price * quantity;
                Console.WriteLine($"{products[i, 0]} | ${totalValue:F2}");
            }
        }
    }
}
