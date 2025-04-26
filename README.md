# freight-aggregators
12 - 14---16
class FreightAggregator:
    def __init__(self):
        self.carriers = []
        self.orders = []
    def register_carrier(self, name, capacity):
        self.carriers.append({"name": name, "capacity": capacity})
        print(f"Перевозчик {name} зарегистрирован с вместимостью {capacity} кг.")
    def create_order(self, order_id, weight):
        self.orders.append({"order_id": order_id, "weight": weight})
        print(f"Создан заказ {order_id} на перевозку {weight} кг.")
    def find_carrier(self, order_id):
        order = next((o for o in self.orders if o["order_id"] == order_id), None)
        if not order:
            print("Заказ не найден.")
            return

        suitable_carriers = [c for c in self.carriers if c["capacity"] >= order["weight"]]
        if not suitable_carriers:
            print("Нет подходящих перевозчиков.")
        else:
            best_carrier = min(suitable_carriers, key=lambda c: c["capacity"])
            print(f"Заказ {order_id} назначен перевозчику {best_carrier['name']}.")

# Пример использования
aggregator = FreightAggregator()
aggregator.register_carrier("Carrier1", 1000)
aggregator.register_carrier("Carrier2", 500)
aggregator.create_order("Order1", 400)
aggregator.create_order("Order2", 800)
aggregator.find_carrier("Order1")
aggregator.find_carrier("Order2")
