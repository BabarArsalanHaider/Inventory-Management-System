# Inventory-Management-System
class Product:
    def __init__(self, product_id, name, category, price, stock_quantity):
        self.product_id = product_id
        self.name = name
        self.category = category
        self.price = price
        self.stock_quantity = stock_quantity

    def __str__(self):
        return f"Product ID: {self.product_id}, Name: {self.name}, Category: {self.category}, Price: {self.price}, Stock: {self.stock_quantity}"

class Inventory:
    def __init__(self):
        self.products = []

    def add_product(self, product):
        self.products.append(product)

    def edit_product(self, product_id, new_name, new_category, new_price, new_stock_quantity):
        for product in self.products:
            if product.product_id == product_id:
                product.name = new_name
                product.category = new_category
                product.price = new_price
                product.stock_quantity = new_stock_quantity
                break
        else:
            print("Product not found")

    def delete_product(self, product_id):
        for i, product in enumerate(self.products):
            if product.product_id == product_id:
                del self.products[i]
                break
        else:
            print("Product not found")

    def view_products(self):
        for product in self.products:
            print(product)

    def search_products(self, query):
        results = []
        for product in self.products:
            if query.lower() in product.name.lower() or query.lower() in product.category.lower():
                results.append(product)
        return results

    def filter_products(self, min_stock):
        results = []
        for product in self.products:
            if product.stock_quantity <= min_stock:
                results.append(product)
        return results

    def adjust_stock(self, product_id, quantity):
        for product in self.products:
            if product.product_id == product_id:
                product.stock_quantity += quantity
                if product.stock_quantity < 10:
                    print(f"Low stock for {product.name}, please restock.")
                break
        else:
            print("Product not found")

def main():
    inventory = Inventory()
    while True:
        print("\nInventory Management System")
        print("1. Add Product")
        print("2. Edit Product")
        print("3. Delete Product")
        print("4. View Products")
        print("5. Search Products")
        print("6. Filter Products")
        print("7. Adjust Stock")
        print("8. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            product_id = input("Enter product ID: ")
            name = input("Enter product name: ")
            category = input("Enter product category: ")
            price = float(input("Enter product price: "))
            stock_quantity = int(input("Enter initial stock quantity: "))
            product = Product(product_id, name, category, price, stock_quantity)
            inventory.add_product(product)
        elif choice == '2':
            product_id = input("Enter product ID to edit: ")
            new_name = input("Enter new name: ")
            new_category = input("Enter new category: ")
            new_price = float(input("Enter new price: "))
            new_stock_quantity = int(input("Enter new stock quantity: "))
            inventory.edit_product(product_id, new_name, new_category, new_price, new_stock_quantity)
        elif choice == '3':
            product_id = input("Enter product ID to delete: ")
            inventory.delete_product(product_id)
        elif choice == '4':
            inventory.view_products()
        elif choice == '5':
            query = input("Enter search query: ")
            results = inventory.search_products(query)
            for product in results:
                print(product)
        elif choice == '6':
            min_stock = int(input("Enter minimum stock level: "))
            results = inventory.filter_products(min_stock)
            for product in results:
                print(product)
        elif choice == '7':
            product_id = input("Enter product ID to adjust stock: ")
            quantity = int(input("Enter quantity to adjust: "))
            inventory.adjust_stock(product_id, quantity)
        elif choice == '8':
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
