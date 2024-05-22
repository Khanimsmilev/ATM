# ATM
ATM system in c#
class ATM
{
    int PIN;
    double balance;

    public ATM()
    {
        PIN = 3589;
        balance = 1000;
    }

    public double CheckBalance()
    {
        return balance;
    }

    /*    public int getPin()
        {
            return PIN;
        }*/
    public void setPin(int pin)
    {
        PIN = pin;
    }
    public bool CheckPin(int pin)
    {

        if (pin != PIN)
        {
            return false;
        }
        else if (pin == PIN)
        {
            return true;
        }
        return false;
    }

    public bool Withdraw(double amount)
    {
        if (amount > balance)
        {
            return false;
        }
        else
        {
            balance -= amount;
            return true;
        }
    }
    public void Increase(double amount)
    {
        balance += amount;
    }

}

class Program
{
    static void Main(string[] args)
    {
        ATM aTM = new ATM();

        int Pin;
        int Choice;
        int Try = 3;
        double Amount;
        do
        {
            Console.WriteLine("Enter PIN: ");
            Pin = Convert.ToInt32(Console.ReadLine());
            bool check = aTM.CheckPin(Pin);

            if (check == true)
            {
                Console.WriteLine("\n\nWelcome!");
                do
                {
                    Console.WriteLine("\nEnter your choice:\n ");
                    Console.WriteLine("1. Show balance;");
                    Console.WriteLine("2. Withdraw money from balance;");
                    Console.WriteLine("3. Increase the balance;");
                    Console.WriteLine("4. Change the Pin.");
                    Console.WriteLine("5. Exit\n");

                    Choice = Convert.ToInt32(Console.ReadLine());

                    switch (Choice)
                    {
                        case 1:
                            Console.WriteLine("\nYour current balance is: " + aTM.CheckBalance()+"\n");
                            break;
                        case 2:
                            Console.WriteLine("\nEnter amount: ");
                            Amount = Convert.ToDouble(Console.ReadLine());
                            check = aTM.Withdraw(Amount);
                            if (check == true)
                            {
                                Console.WriteLine("Amount withdrawn: " + Amount+"\n");
                            }
                            else
                            {
                                Console.WriteLine("\nInsufficient balance!\n");
                            }
                            break;
                        case 3:
                            Console.WriteLine("\nEnter amount: ");
                            Amount = Convert.ToDouble(Console.ReadLine());
                            aTM.Increase(Amount);
                            Console.WriteLine("\nBalance increased successfully!\n");
                            break;
                        case 4:
                            Console.WriteLine("\nEnter new Pin: \n");
                            Pin = Convert.ToInt32(Console.ReadLine());
                            aTM.setPin(Pin);
                            Console.WriteLine("\nPin changed successfully!\n");
                            break;
                        case 5:
                            Console.WriteLine("\nExited successfully!\n");
                            break;
                        default:
                            Console.WriteLine("\nIncorrect input!\n");
                            break;

                    }
                } while (Choice != 5);

            }

            else if (check == false)
            {
                Console.WriteLine("\nIncorrect Pin!");
                --Try;
            }


        } while (Try != 0);
        Console.WriteLine("\nYou have run out of attempts!");
    }

}

