using System;
using System.Transactions;
namespace FinalProject
{
    class BudgetTracker
    {
        private static string description;

        static void Main(string[] args)
        {
            List<Transaction> transactions = new List<Transaction>();
            bool exit = false;
            Console.WriteLine("Welcome to the Personal Budget Tracker");

            while(!exit)
            {
                Console.WriteLine("\n Choose Your Option");
                Console.WriteLine("1.Add Income");
                Console.WriteLine("2.Add Expense");
                Console.WriteLine("3.View Transaction");
                Console.WriteLine("4.View Total Balance");
                Console.WriteLine("5.Exit");

                Console.Write("Enter Your Choose");
                string choice = Console.ReadLine();

                switch(choice)
                {
                    case "1":
                        AddTransaction(transactions, "Income");
                    break;

                    case "2":
                        AddTransaction(transactions, "Expense");
                    break;

                    case "3":
                        ViewTransaction(transactions);
                    break;

                    case "4":
                        ViewBalance(transactions);
                    break;

                    case "5":

                        exit = true;
                        Console.WriteLine("Thank You");
                    break ;

                    default:
                        Console.WriteLine("Invalid Choice!. PLEASE TRY AGAIN");
                    break;
                }
            }
        }
        static void AddTransaction(List<Transaction>transactions, string type)
        {
            Console.WriteLine($"Enter the {type}description:");
            if(decimal.TryParse(Console.ReadLine(), out decimal amount))
            {
                if (type == "Expense")
                {
                    amount = - amount;
                }
                transactions.Add(new Transaction(type, description, amount));
                Console.WriteLine($"{type} added successfully!");
            }
            else
            {
                Console.WriteLine("Invalid amount.Try again");
            }
        }

        static void ViewTransaction(List<Transaction> transactions)
        {
            Console.WriteLine("\n Your Transaction:");
            if (transactions.Count == 0)
            {
                Console.WriteLine("No transaction recorded yet");
            }
            else
            {
                foreach (var transaction in transactions)
                {
                    Console.WriteLine($"{transaction.Type}: {transaction.Description}-{transaction.Amount}");
                }
            }
        }

        static void ViewBalance(List<Transaction> transactions)
        {
            decimal totalBalance = 0;
            foreach(var transaction in transactions)
            {
                totalBalance += transaction.Amount;

            }

            Console.WriteLine($"\n Total Balance{totalBalance}");
        }
    }
    class Transaction
    {
        public string Description { get; set; }
        public string Type { get; set; }
        public decimal Amount { get; set; }

        public Transaction(string type , string description , decimal amount)
        {
            Description = description;
            Type = type;
            Amount = amount;
        }
    }

   
     
}
