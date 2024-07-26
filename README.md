# SAHIL 
This the repository of a basic hotel management program in C programming..

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_FOOD_ITEMS 200
#define MAX_ORDER_ITEMS 200
#define MAX_ROOMS 10

void begin(); /* Function declarations */
void program();
void show_details();
void complaints_suggestions();
void book_room();
void mini_casino();
void GuessGame(int amount_bet, int *inhand_cash);
void food_items(void);
void initialize_menu(void);

typedef struct
{
    char name[50];
    int price;
} FoodItem;

FoodItem menu[MAX_FOOD_ITEMS];
int total_food_items = 0; // To keep track of the number of food items added

typedef struct
{
    char name[50];
    int quantity;
    int price;
} OrderedFoodItem;

OrderedFoodItem ordered_items[MAX_ORDER_ITEMS];
int total_order_items = 0; // To keep track of the number of ordered items

typedef struct
{
    int roomno;
    char *roomtype;
    int price;
} RoomBooking;

RoomBooking bookings[MAX_ROOMS];
int total_bookings = 0; // To keep track of the number of rooms booked

typedef struct
{ /* Structure that stores details of persons */
    char name[20];
    char address[50];
    char email_id[30];
    char nationality[25];
    int room_bill;
    int food_bill;
    int program_bill;
    char *programs[10]; // Array to hold multiple programs
    int program_count;  // Number of programs chosen
} Person;

Person person;

int main()
{
    initialize_menu(); // Initialize the food menu
    person.room_bill = 0;
    person.food_bill = 0;
    person.program_bill = 0;
    person.program_count = 0; // Initialize the program count
    printf(".............WELCOME TO GHUMTEE RIVERA RESTAURANT AND LODGE..............\n");
    printf("Please enter your details before moving to the main page!\n");
    printf("Please enter your name: ");
    scanf(" %[^\n]", person.name);
    printf("Enter your address: ");
    scanf(" %[^\n]", person.address);
    printf("Enter your nationality: ");
    scanf(" %[^\n]", person.nationality);
    printf("Enter your email_id: ");
    scanf(" %[^\n]", person.email_id);
    begin();
    return 0;
}

void initialize_menu(void)
{
    // Example food items - Add up to 200 items
    strcpy(menu[0].name, "Burger");
    menu[0].price = 150;

    strcpy(menu[1].name, "Pizza");
    menu[1].price = 300;

    strcpy(menu[2].name, "Pasta");
    menu[2].price = 250;

    // Continue adding items up to menu[MAX_FOOD_ITEMS - 1]
    total_food_items = 3; // Update with the actual number of items added
}

void begin(void)
{
    int decide;
    printf("\n-----------------------HOME PAGE--------------------------\n");
    printf("\n            HOW CAN WE HELP YOU?\n\n");
    printf("\n1. Book a room\n2. Program\n3. Mini casino\n4. Food items\n5. Show my details\n6. Complaints or suggestions\n7. Check out\n8. About us\n");
    scanf("%d", &decide);
    while (getchar() != '\n'); // Clear input buffer

    switch (decide)
    {
    case 1:
        book_room();
        break;
    case 2:
        program();
        break;
    case 3:
        mini_casino();
        break;
    case 4:
        food_items();
        break;
    case 5:
        show_details();
        break;
    case 6:
        complaints_suggestions();
        printf("Thank you for your valuable suggestions!\n");
        begin();
        break;
    case 7:
        printf("Visit again!\n");
        printf("Thank you for trusting our service.\n");
        return; // Exit the function to stop further execution
    case 8:
        printf("GHUMTEE RIVERA RESORT:\n");
        printf("A beautiful cosmopolitan destination for a picturesque natural scenario, a blend of Natural and Artificial effort located on the border of");
        printf("Chitwan National Park (A UNESCO World Heritage Site) allows you to enjoy the breeze of Rapti River flowing through the lap of Chitwan National Park.");
        printf("Enjoying the spectacular sunset and its reflection on Rapti River along with grazing of deer on the bank by relaxing on our rugged cottages");
        printf("is the memorable experience you could enjoy only at GHUMTEE RIVERA RESORT.\n");
        printf("We would be more than happy to experience you Jungle Safari, canoe ride to Crocodile Breeding Farm, and Ox-Cart ride.");
        printf("Clean and Comfortable rooms, Hot and Cold Water facilities, beautiful garden, family environment, and local food are our salient features to give you a taste of our Nepalese Culture.");
        printf("Satisfying you totally with our unique culture is our primary motto.\n");
        begin();
        break;
    default:
        printf("Invalid choice! Please try again.\n");
        begin();
    }
}

void book_room(void)
{
    int type_of_rooms, quantity;
    char c;

    printf("\nHow many rooms do you want to book? (Max %d): ", MAX_ROOMS - total_bookings);
    scanf("%d", &quantity);
    while (getchar() != '\n'); // Clear input buffer

    if (quantity > MAX_ROOMS - total_bookings)
    {
        printf("Sorry, we only have space for %d more rooms.\n", MAX_ROOMS - total_bookings);
        begin();
    }
    
    for (int i = 0; i < quantity; i++)
    {
        printf("\nRoom %d:\n", i + 1);
        printf("What type of room do you want to book?\n");
        printf("\n1. Basic Room    Rs 1000\n2. Medium room   Rs 2000\n3. DELUXE ROOM   Rs 3000\n4. Cancel Booking\n");
        scanf("%d", &type_of_rooms);
        while (getchar() != '\n'); // Clear input buffer

        if (type_of_rooms == 1)
        {
            printf("\nDo you accept this room? (y/n)\n");
            scanf("%c", &c);
            while (getchar() != '\n'); // Clear input buffer
            if (c == 'y')
            {
                printf("\nYou chose the basic room. Enjoy your stay\n");
                bookings[total_bookings].roomno = 121 + total_bookings;
                bookings[total_bookings].roomtype = "basic";
                bookings[total_bookings].price = 1000;
                person.room_bill += 1000;
                total_bookings++;
            }
        }
        else if (type_of_rooms == 2)
        {
            printf("\nDo you accept this room? (y/n)\n");
            scanf("%c", &c);
            while (getchar() != '\n'); // Clear input buffer
            if (c == 'y')
            {
                printf("\nYou chose the medium room. Enjoy your stay\n");
                bookings[total_bookings].roomno = 121 + total_bookings;
                bookings[total_bookings].roomtype = "medium";
                bookings[total_bookings].price = 2000;
                person.room_bill += 2000;
                total_bookings++;
            }
        }
        else if (type_of_rooms == 3)
        {
            printf("\nDo you accept this room? (y/n)\n");
            scanf("%c", &c);
            while (getchar() != '\n'); // Clear input buffer
            if (c == 'y')
            {
                printf("\nYou chose the deluxe room. Enjoy your stay\n");
                bookings[total_bookings].roomno = 121 + total_bookings;
                bookings[total_bookings].roomtype = "deluxe";
                bookings[total_bookings].price = 3000;
                person.room_bill += 3000;
                total_bookings++;
            }
        }
        else if (type_of_rooms == 4)
            break;
        else
            printf("Invalid choice. Please try again.\n");
    }

    begin();
}

void program(void)
{
    int p;
    printf("\nWhich program(s) do you want to choose? (Enter multiple numbers separated by spaces, and 0 to finish)\n");
    printf("\n1. Jungle Walk - Rs 1000\n2. Jungle Jeep Drive - Rs 2000\n3. Canoe Ride - Rs 800\n4. Cultural Show - Rs 1000\n");
    
    while (1)
    {
        scanf("%d", &p);
        while (getchar() != '\n'); // Clear input buffer

        if (p == 0)
            break;

        switch (p)
        {
        case 1:
            printf("\nYou chose Jungle Walk\n");
            person.programs[person.program_count] = "Jungle Walk";
            person.program_bill += 1000;
            person.program_count++;
            break;
        case 2:
            printf("\nYou chose Jungle Jeep Drive\n");
            person.programs[person.program_count] = "Jungle Jeep Drive";
            person.program_bill += 2000;
            person.program_count++;
            break;
        case 3:
            printf("\nYou chose Canoe Ride\n");
            person.programs[person.program_count] = "Canoe Ride";
            person.program_bill += 800;
            person.program_count++;
            break;
        case 4:
            printf("\nYou chose Cultural Show\n");
            person.programs[person.program_count] = "Cultural Show";
            person.program_bill += 1000;
            person.program_count++;
            break;
        default:
            printf("Invalid choice. Please try again.\n");
        }
    }

    begin();
}

void show_details(void)
{
    printf("\nYour details are as follows:\n");
    printf("Name        : %s\n", person.name);
    printf("Email id    : %s\n", person.email_id);
    printf("Address     : %s\n", person.address);

    printf("Room Bookings:\n");
    for (int i = 0; i < total_bookings; i++)
    {
        printf("Room No: %d, Room Type: %s, Price: Rs %d\n", bookings[i].roomno, bookings[i].roomtype, bookings[i].price);
    }

    if (person.program_count > 0)
    {
        printf("Programs    : ");
        for (int i = 0; i < person.program_count; i++)
        {
            printf("%s", person.programs[i]);
            if (i < person.program_count - 1)
                printf(", ");
        }
        printf("\n");
    }
    
    if (total_order_items > 0)
    {
        printf("Ordered Food:\n");
        for (int i = 0; i < total_order_items; i++)
        {
            printf("%s - %d x Rs %d\n", ordered_items[i].name, ordered_items[i].quantity, ordered_items[i].price);
        }
    }
    
    printf("\nDetailed Bills:\n");
    printf("Room Bill    : Rs %d\n", person.room_bill);
    
    int food_total = 0;
    for (int i = 0; i < total_order_items; i++)
    {
        food_total += ordered_items[i].quantity * ordered_items[i].price;
    }
    person.food_bill = food_total;
    printf("Food Bill    : Rs %d\n", person.food_bill);
    
    printf("Program Bill : Rs %d\n", person.program_bill);
    
    int total_bill = person.room_bill + person.food_bill + person.program_bill;
    printf("Total Bill   : Rs %d\n", total_bill);
    
    printf("Press Enter to continue...");
    getchar(); // Wait for user input
    while (getchar() != '\n'); // Consume newline character left by previous input
    begin();
}

void complaints_suggestions(void)
{
    char complain[500];
    printf("Please enter your complaints or suggestions:\n");
    scanf(" %[^\n]", complain); // Read until newline
    printf("Your complaints or suggestions have been recorded.\n");
    begin();
}

void GuessGame(int amount_bet, int *inhand_cash)
{
    char num[3] = {'N', 'R', 'N'};
    printf("\nWait!! Number is shuffling its position...\n");
    int i, x, y, temp; /* Swapping the number's position five times using random number for random index */
    for (i = 0; i < 5; i++)
    {
        x = rand() % 3;
        y = rand() % 3;
        temp = num[x];
        num[x] = num[y];
        num[y] = temp;
    }
    int PlayerGuess;
    printf("\nYou may now guess the number in which R is present: ");
    scanf("%d", &PlayerGuess);
    if (num[PlayerGuess - 1] == 'R')
    {
        (*inhand_cash) += 2 * amount_bet;
        printf("You win! The numbers are as follows: ");
        printf("\"%c %c %c\" ", num[0], num[1], num[2]);
        printf("\nYour inhand_cash is now = %d \n", *inhand_cash);
    }
    else
    {
        (*inhand_cash) -= amount_bet;
        printf("You lose! The numbers are as follows: ");
        printf("\"%c %c %c\" ", num[0], num[1], num[2]);
        printf("\nYour inhand_cash is now = %d \n", *inhand_cash);
    }
}

void mini_casino()
{
    int amount_bet, inhand_cash; /* You have to guess the right number among 3 numbers. The position where right number is is named as 'R' and rest two are named as 'N'. If your guess is wrong, you lose the amount_bet from your inhand_cash. If you guess it right, you win twice the amount_bet in your inhand_cash. Keep playing and keep winning until you go out of cash */
    printf("\n////////-WELCOME TO MINI CASINO-\\\\\\\\\\\\ \n");
    printf("\n----Enter the inhand_cash you have right now---- :\n ");
    scanf("%d", &inhand_cash);
    while (getchar() != '\n'); // Clear input buffer
    while (inhand_cash > 0)
    {
        printf("\nEnter the amount_bet you want to play for : \n");
        scanf("%d", &amount_bet);
        while (getchar() != '\n'); // Clear input buffer
        if (amount_bet > inhand_cash)
        {
            printf("Insufficient cash. Exiting the game.\n");
            break;
        }
        else
        {
            GuessGame(amount_bet, &inhand_cash);
        }
    }
    if (inhand_cash == 0)
    {
        printf("\n\"Sorry you don't have enough cash to play more,\nDo come next time\"\n\n");
        printf("\nThank you for playing\n");
    }
    begin();
}

void food_items(void)
{
    int choice, quantity;
    int item_found = 0;

    printf("\n------------FOOD MENU------------\n");
    for (int i = 0; i < total_food_items; i++)
    {
        printf("%d. %s - Rs %d\n", i + 1, menu[i].name, menu[i].price);
    }
    printf("Enter the number of the food item you want to order (0 to finish): ");
    scanf("%d", &choice);
    while (getchar() != '\n'); // Clear input buffer

    while (choice != 0)
    {
        if (choice > 0 && choice <= total_food_items)
        {
            printf("Enter the quantity for %s: ", menu[choice - 1].name);
            scanf("%d", &quantity);
            while (getchar() != '\n'); // Clear input buffer

            person.food_bill += menu[choice - 1].price * quantity;

            // Record the ordered food item
            int found = 0;
            for (int i = 0; i < total_order_items; i++)
            {
                if (strcmp(ordered_items[i].name, menu[choice - 1].name) == 0)
                {
                    ordered_items[i].quantity += quantity;
                    found = 1;
                    break;
                }
            }
            if (!found)
            {
                strcpy(ordered_items[total_order_items].name, menu[choice - 1].name);
                ordered_items[total_order_items].quantity = quantity;
                ordered_items[total_order_items].price = menu[choice - 1].price;
                total_order_items++;
            }

            printf("Added %d x %s to your bill.\n", quantity, menu[choice - 1].name);
            item_found = 1;
        }
        else
        {
            printf("Invalid choice. Please try again.\n");
        }

        printf("Enter the number of the food item you want to order (0 to finish): ");
        scanf("%d", &choice);
        while (getchar() != '\n'); // Clear input buffer
    }

    if (!item_found)
    {
        printf("No items were selected.\n");
    }

    begin();
}

