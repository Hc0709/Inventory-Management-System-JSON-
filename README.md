# Inventory-Management-System-JSON-
The Inventory Management System is a Python-based console application designed to efficiently manage inventory, track sales, and handle customer interactions. Leveraging file handling capabilities, this system ensures accurate and organized data management, making it an essential tool for any retail or wholesale business. (JSON)

```markdown
# Inventory Management and Billing System

This is a simple inventory management and billing system implemented in Python. The system reads product data from a JSON file, processes sales, and updates the inventory accordingly. It also generates sales records and stores them in a separate file.

## Features

- **Load Inventory**: Reads inventory data from a JSON file.
- **Save Inventory**: Writes updated inventory data back to the JSON file.
- **Billing Process**: Generates bills for customer purchases and updates inventory.
- **Sales Record**: Maintains a record of sales in a separate file.

## File Structure

### `records.json`

The `records.json` file should contain the inventory data in the following format:

```json
{
    "1001": {"name": "5star", "Price": 10, "quan": 100},
    "1002": {"name": "silk", "Price": 100, "quan": 50},
    "1003": {"name": "twix", "Price": 30, "quan": 150},
    "1004": {"name": "milkybar", "Price": 40, "quan": 110},
    "1005": {"name": "galaxy", "Price": 20, "quan": 100}
}
```

### `sales.txt`

The `sales.txt` file will store the sales records in CSV format.

## Usage

### Prerequisites

- Python 3.x

### Running the System

1. **Reading Inventory**: Reads the inventory from the `records.json` file and stores it in a dictionary.

```python
import json

fd = open("records.json", 'r')
js = fd.read()
fd.close()

records = json.loads(js)
```

2. **Displaying Menu**: Displays the available products.

```python
print("________________MENU__________________")

for key in records.keys():
    print(key, ":", records[key]['name'], '|', records[key]['Price'], '|', records[key]['quan'])

print("______________________________________")
```

3. **User Input**: Collects user information and desired product details.

```python
user_name = str(input("Enter your name          :"))
user_email = str(input("Enter your email         :"))
user_phno = str(input("Enter your phone number  :"))
uid = str(input("Enter product ID         :"))
quantity = int(input("Enter the quantity       :"))
```

4. **Processing Sales**: Processes the sale, updates inventory, and generates a sales record.

```python
import time

if records[uid]['quan'] >= quantity:
    print("_______________________________________")
    print("            BILL DETAILS                ")
    print("Name      :", records[uid]['name'])
    print("Price     :", records[uid]['Price'], "rs")
    print("Quantity  :", quantity)
    print("__________________________________________")
    print("Billing amount :", records[uid]['Price'] * quantity, "rs")
    print("__________________________________________")

    if records[uid]['Price'] * quantity > 1000:
        print("Discount =", int(records[uid]['Price'] * quantity) - 100)

    sales = '1'+","+user_name+","+user_email+","+user_phno+","+uid+","+records[uid]['name']+","+str(quantity)+","+str(quantity*records[uid]['Price'])+','+time.ctime()+'\n'
    records[uid]['quan'] -= quantity
else:
    print("Sorry, we do not have enough quantity in our inventory")
    print("We are only having", records[uid]['quan'], "available")
    print("_______________________________________")
    
    ch = str(input("Press Y/y to purchase"))
    
    if records[uid]['quan'] == 0:
        print("No items available sorry!!!")

    if ch == 'y' or ch == 'Y':
        print("_______________________________________")
        print("            BILL DETAILS                ")
        print("Name      :", records[uid]['name'])
        print("Price     :", records[uid]['Price'], "rs")
        print("Quantity  :", records[uid]['quan'])
        print("__________________________________________")
        print("Billing amount :", records[uid]['Price'] * records[uid]['quan'], "rs")
        print("__________________________________________")

        sales = '1'+","+user_name+","+user_email+","+user_phno+","+uid+","+records[uid]['name']+","+str(records[uid]['quan'])+","+str(records[uid]['quan']*records[uid]['Price'])+','+time.ctime()+'\n'
        records[uid]['quan'] = 0
    else:
        print('Thank you!!!')
```

5. **Saving Records**: Converts the dictionary back to a JSON string and saves it to the `records.json` file. Also, appends the sales record to the `sales.txt` file.

```python
js = json.dumps(records)

fd = open("records.json", "w")
fd.write(js)
fd.close()

fd = open('sales.txt', 'a')
fd.write(sales)
fd.close()

print("__________________________________________")
print("Thanks for your order. Inventory updated.")
print("__________________________________________")
```

## Contributing

Feel free to fork this repository and submit pull requests. Contributions are welcome!

## License

This project is licensed under the MIT License.
```

You can use this `README.md` file to provide a clear overview of your project, its features, and how to use it.
