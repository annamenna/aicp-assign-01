# aicp-assign-01
# Function to display available items and get user choice
def get_user_choice(category, items):
    print(f"\n{category} Options:")
    for i, item in enumerate(items):
        print(f"{i + 1}. {item[1]} - ${item[2]:.2f}")

    choice = int(input(f"Select a {category} (1-{len(items)}): "))
    return items[choice - 1]

# Function to calculate the price of the computer
def calculate_computer_price(selected_items):
    base_price = 200
    total_price = base_price + sum(item[2] for item in selected_items)
    return total_price

# Main program
case_options = [
    ["A1", "Compact", 75.00],
    ["A2", "Tower", 150.00]
]

ram_options = [
    ["B1", "8 GB", 79.99],
    ["B2", "16 GB", 149.99],
    ["B3", "32 GB", 299.99]
]

hdd_options = [
    ["C1", "1 TB HDD", 49.99],
    ["C2", "2 TB HDD", 89.99],
    ["C3", "4 TB HDD", 129.99]
]

# Initialize selected items array
selected_items = []

# Step 1: Choose one case, one RAM, and one Main Hard Disk Drive
selected_items.append(get_user_choice("Case", case_options))
selected_items.append(get_user_choice("RAM", ram_options))
selected_items.append(get_user_choice("Main Hard Disk Drive", hdd_options))

# Calculate initial computer price
computer_price = calculate_computer_price(selected_items)

# Step 2: Allow a customer to choose whether to purchase additional items
additional_items = input("Do you want to purchase additional items? (yes/no): ").lower()

if additional_items == "yes":
    # Additional items categories
    ssd_options = [
        ["D1", "240 GB SSD", 59.99],
        ["D2", "480 GB SSD", 119.99]
    ]

    second_hdd_options = [
        ["E1", "1 TB HDD", 49.99],
        ["E2", "2 TB HDD", 89.99],
        ["E3", "4 TB HDD", 129.99]
    ]

    optical_drive_options = [
        ["F1", "DVD/Blu-Ray Player", 50.00],
        ["F2", "DVD/Blu-Ray Re-writer", 100.00]
    ]

    os_options = [
        ["G1", "Standard Version", 100.00],
        ["G2", "Professional Version", 175.00]
    ]

    # Allow the customer to choose additional items
    selected_items.append(get_user_choice("Solid State Drive", ssd_options))
    selected_items.append(get_user_choice("Second Hard Disk Drive", second_hdd_options))
    selected_items.append(get_user_choice("Optical Drive", optical_drive_options))

    # Ask if the customer wants an operating system
    os_choice = input("Do you want to include an Operating System? (yes/no): ").lower()
    if os_choice == "yes":
        selected_items.append(get_user_choice("Operating System", os_options))

    # Calculate the updated computer price
    updated_computer_price = calculate_computer_price(selected_items)

    # Step 3: Apply discounts based on the number of additional items
    num_additional_items = len(selected_items) - 3  # Subtracting the initially chosen items

    discount_percentage = 0
    if num_additional_items == 1:
        discount_percentage = 5
    elif num_additional_items >= 2:
        discount_percentage = 10

    discount_amount = (discount_percentage / 100) * updated_computer_price
    discounted_price = updated_computer_price - discount_amount

    # Output the final details
    print("\nChosen Items:")
    for item in selected_items:
        print(f"{item[1]} - ${item[2]:.2f}")

    print(f"\nInitial Computer Price: ${computer_price:.2f}")
    print(f"Updated Computer Price: ${updated_computer_price:.2f}")
    print(f"Discount Applied: {discount_percentage}%")
    print(f"Discount Amount: ${discount_amount:.2f}")
    print(f"Final Price after Discount: ${discounted_price:.2f}")

else:
    # Output the final details without additional items
    print("\nChosen Items:")
    for item in selected_items:
        print(f"{item[1]} - ${item[2]:.2f}")

    print(f"\nComputer Price: ${computer_price:.2f}")
    print("No additional items purchased.")
