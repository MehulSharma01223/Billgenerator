# Billgenerator
This project is a humorous yet educational Python script that generates a restaurant bill with hidden charges, applying various Python data structures and control flow concepts.
# ==========================================
# PROJECT: THE 'FINE PRINT' BILL GENERATOR
# ==========================================

print("--- WELCOME TO THE 'LUXURY' DINER ---")
print("(Where you pay for the food... and the air you breathe)")

# 1. TUPLES (Immutable Menu)
# The menu is fixed. Format: (Item Name, Price)
MENU = (
    ("Mineral Water", 50),
    ("Cheese Pasta", 350),
    ("Spicy Burger", 200),
    ("Lava Cake", 250),
    ("Garlic Bread", 150)
)

# 2. DICTIONARY (Hidden Charges Database)
# Rules for extra fees.
# 'Fixed' means a flat rupee amount. 'Percent' is a multiplier.
HIDDEN_FEES = {
    "Sitting Fee": 50,              # Charge for using the chair
    "Ambiance Tax": 30,             # Charge for the music
    "Cutlery Rental": 20,           # Charge for using a fork
    "Service Charge": 0.10          # 10% of the total bill
}

# 3. LIST (The Order)
# Keeps the sequence of items ordered.
cart = []

# 4. SET (Unique Checker)
unique_items = set()

while True:
    print("\n--- MENU ---")
    # Session 2: Enumerate Loop
    for i, item in enumerate(MENU):
        print(f"{i+1}. {item[0]} \t(Rs. {item[1]})")
    
    print("6. Generate Bill (Stop Ordering)")
    
    try:
        choice = int(input("Select Item Number: "))
        
        if choice == 6:
            break
            
        if 1 <= choice <= 5:
            selected_item = MENU[choice-1]
            item_name = selected_item[0]
            item_price = selected_item[1]
            
            # Add to List (Cart)
            cart.append(selected_item)
            
            # Add to Set (Unique Tracker)
            unique_items.add(item_name)
            
            print(f"Added {item_name} to cart.")
        else:
            print("Invalid choice!")
            
    except ValueError:
        print("Please enter a number.")

 # --- BILL GENERATION ---
print("\n" + "="*40)
print("       FINAL INVOICE       ")
print("="*40)

if not cart:
    print("You didn't order anything... but here is a fee for wasting our time.")
    base_total = 0
else:
    base_total = 0
    print("Items Ordered:")
    
    # Calculate Base Total
    for item in cart:
        print(f" - {item[0]:<15} Rs. {item[1]}")
        base_total += item[1]

    print(f"\nFood Total:\t\t Rs. {base_total}")
    
    # --- APPLYING HIDDEN CHARGES (The Logic) ---
    extra_charges_total = 0
    
    # 1. Flat Fees (Always applied)
    print("\n--- EXTRA CHARGES (Surprise!) ---")
    
    # Apply Ambiance & Sitting Fee
    print(f" + Sitting Fee:\t\t Rs. {HIDDEN_FEES['Sitting Fee']}")
    print(f" + Ambiance Tax:\t\t Rs. {HIDDEN_FEES['Ambiance Tax']}")
    extra_charges_total += HIDDEN_FEES['Sitting Fee'] + HIDDEN_FEES['Ambiance Tax']
    
    # 2. Conditional Fee (Using SET Logic)
    # If they ordered more than 2 UNIQUE types of dishes, charge for "Table Space"
    if len(unique_items) > 2:
        print(f" + Table Space Fee:\t Rs. 100 (You ordered too many dishes)")
        extra_charges_total += 100
        
    # 3. Percentage Fee (Service Charge)
    # 10% of the Food Total
    svc_charge = base_total * HIDDEN_FEES['Service Charge']
    print(f" + Service Charge (10%):\t Rs. {svc_charge:.2f}")
    extra_charges_total += svc_charge

    # --- GST CALCULATION (Session 1 Math) ---
    # GST is 18% of the (Food + Extras)
    sub_total = base_total + extra_charges_total
    gst_amount = sub_total * 0.18
    
    print("-" * 40)
    print(f"Sub Total:\t\t Rs. {sub_total:.2f}")
    print(f"GST (18%):\t\t Rs. {gst_amount:.2f}")
    
    final_bill = sub_total + gst_amount
    
    print("=" * 40)
    print(f"GRAND TOTAL:\t\t Rs. {final_bill:.2f}")
    print("=" * 40)
    print("Thank you for being rich!")
