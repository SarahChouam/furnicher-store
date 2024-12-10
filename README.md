import json 

from datetime import datetime 

 

class Furnicher: 
#the atributes of the furnichers
    def __init__(self, id, name, category, attributes, quantity): 

        self.id = id 

        self.name = name 

        self.category = category 

        self. attributes = attributes 

        self.quantity = quantity 

         
#to add furnichers
    def update_quantity(self, amount): 

        self.quantity += amount 

#returns furnicher details       

    def info(self): 

        return f"ID: {self.id},name: {self.name}, category: {self.category}, attributes: {self.attributes}, quantity: {self.quantity}" 

     

class Inventory: 

    def __init__(self): 

        self.furnichers = [] 

         
#add furnicher to inventory
    def add_furnicher(self, furnicher): 

        self.furnichers.append(furnicher) 

         
#remove furnicher from inventory
    def remove_furnicher(self, furnicher_id): 

        self.furnichers = [furnicher for furnicher in self.furnichers if furnicher.id != furnicher_id] 

         
#gets furnichers by the id
    def get_furnicher(self, furnicher_id): 

        for furnicher in self.furnichers: 

            if furnicher.id == furnicher_id: 

                 

                return furnicher 

        return None 

     
#turns list of (info()) furnichers in the inventory
    def furnicher_list(self): 

        return [furnicher.info() for furnicher in self.furnichers] 

     
#updates inventory
    def update_invertory(self, furnicher_id, amount): 

        furnicher = self.get_furnicher(furnicher_id) 

        if furnicher: 

            furnicher.update_quantity(amount) 

             
#checks and returns quantity of furnichers
    def stock(self, furnicher_id): 

        furnicher = furnicher.get_furnicher(furnicher_id) 

        return furnicher.quantity if furnicher else None 

     

class Report: 

    def __init__(self,inventory): 

        self.inventory = inventory 

#returns furnichers with low stock        

    def low_stock(self, threshold): 

        return [furnicher.info() for furnicher in self.inventory.furnichers if furnicher.quantity < threshold] 


     
#returns dict amout of furnichers in stock
    def get_report(self): 

        return  {'furnicher in stock': len(self.inventory.furnicher), 

                 'low_stock': self.low_stock(3)} 

     

class User: 

    def __init__(self, username, role): 

        self.username = username 

        self.role = role 

 
#checks if the user name is correct
    def login(self, username, password): 

        return self.username == username 

 
#gives permission to admin
    def permissions(self): 

        return "Full permissions" if self.role == 'admin' else "Limited permissions" 

 
#lets admin add or remove furnichers
    def inventory_actions(self, action, furnicher): 

        if self.role == 'admin': 

            if action == 'add': 

                inventory.add_furnicher(furnicher) 

            elif action == 'remove': 

                inventory.remove_furnicher(furnicher.id) 

 
#object to recall the class
inventory = Inventory() 

#object to recall the class
report = Report(inventory) 

 

furnicher1 = Furnicher( id= 1, name= "bed", category= "bedroom furnicher", attributes= {"size":"king, queen, twin, double", "color": "white, black, dark brown", "material":"oak"}, quantity= 1) 

furnicher2= Furnicher( id= 2, name= "chair", category= "dining room furnicher", attributes= {"color": "white, black, dark brown", "material":"oak"}, quantity= 1) 

 #add furnicher1 

inventory.add_furnicher(furnicher1) 

#add furnicher2

inventory.add_furnicher(furnicher2) 
 

print(report.low_stock(3)) 




#code structure
+-------------------+       +-----------------+       +-----------------+
|   Furnicher       |       |    Inventory    |       |     Report      |
+-------------------+       +-----------------+       +-----------------+
| - id: int         |<----->| - furnichers: []|<----->| - inventory: obj|
| - name: str       |       +-----------------+       +-----------------+
| - category: str   |       | + add_furnicher()|       | + low_stock()    |
| - attributes: dict|       | + remove_furnicher() |    | + get_report()   |
| - quantity: int   |       | + get_furnicher()|       +-----------------+
+-------------------+       | + furnicher_list()|        
                           | + update_inventory() |
                           | + stock()             |
                           +---------------------+
                               
+------------------+    
|      User        |
+------------------+
| - username: str  |
| - role: str      |
+------------------+
| + login()        |
| + permissions()  |
| + inventory_actions()|
+------------------+

#flowchart
  +---------------+
  |   User Logs   |
  |    In         |
  +---------------+
         |
  +------v------+
  | Check Role  |
  +------v------+
         |
  +------v------+
  |   Admin?    | <-----------+ 
  +------v------+
    Yes   |   No
    |     |
  +---v-----+  +------------+
  | Inventory |  | View Stock|
  | Actions   |  |  & Reports|
  +-----------+  +------------+

 
