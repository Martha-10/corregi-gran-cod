# Lista para almacenar los productos
productos = []

# Función para agregar un producto al inventario
def agregar_producto(nombre, precio, cantidad):
    for producto in productos:
        if producto["Nombre"] == nombre:
            producto["Cantidad"] += cantidad
            print("\nProducto ya existente. Se le ha sumado la cantidad que ingresó.")
            return
    producto = {"Nombre": nombre,
                "Precio": precio,
                "Cantidad": cantidad}
    productos.append(producto)
    print("\nProducto añadido correctamente.")

# Función para consultar un producto en el inventario
def consultar_producto(nombre):
    for producto in productos:
        if producto["Nombre"] == nombre:
            print(f"\nNombre: {producto['Nombre']}")
            print(f"Precio: {producto['Precio']}")
            print(f"Cantidad: {producto['Cantidad']}")
            return
    print(f"\nError. El producto '{nombre}' no se encuentra en la lista de productos almacenados.")

# Función para actualizar el precio de un producto
def actualizar_precio(nombre, precio):
    for producto in productos:
        if producto["Nombre"] == nombre:
            producto["Precio"] = precio
            print("\nPrecio actualizado correctamente.")
            return
    print(f"\nError. El producto '{nombre}' no se encuentra en la lista de productos almacenados.")

# Función para eliminar un producto del inventario
def eliminar_producto(nombre):
    for producto in productos:
        if producto["Nombre"] == nombre:
            productos.remove(producto)
            print(f"\nProducto '{nombre}' eliminado correctamente.")
            return
    print(f"\nError. El producto '{nombre}' no se encuentra en la lista de productos almacenados.")

# Función para mostrar el inventario actual
def mostrar_inventario():
    if not productos:
        print("\nEl inventario está vacío.")
        return
    print(f"\n{'Nombre':<20} {'Precio':<20} {'Cantidad':<20}")
    print("-" * 60)
    for producto in productos:
        print(f"{producto['Nombre']:<20} {producto['Precio']:<20.2f} {producto['Cantidad']:<20}")

# Función lambda para calcular el valor total del inventario
total_del_inventario = lambda: sum(producto["Precio"] * producto["Cantidad"] for producto in productos)

# Bucle principal del programa
while True:
    print("\n1. Añadir producto")
    print("2. Consultar producto")
    print("3. Actualizar precio")
    print("4. Eliminar producto")
    print("5. Calcular valor total del inventario")
    print("6. Mostrar inventario")
    print("7. Salir")

    while True:
        try:
            opcion = input("\nIngrese la opción que desea ejecutar: ")
            opcion = int(opcion)
            break
        except ValueError:
            print("\nError. Ingrese un número válido según la opción que desea.")

    match opcion:
        case 1:
            while True:
                nombre = input("\nIngrese el nombre del producto: ").strip().lower()
                if nombre == "":
                    print("\nError. El nombre del producto no puede estar vacío.")
                else:
                    break

            while True:
                try:
                    precio = input("\nIngrese el precio del producto: ")
                    precio = float(precio)
                    if precio <= 0:
                        print("\nError. El precio del producto debe ser mayor a 0.")
                    else:
                        break
                except ValueError:
                    print("\nError. El precio del producto debe ser un número.")

            while True:
                try:
                    cantidad = input("\nIngrese la cantidad del producto: ")
                    cantidad = int(cantidad)
                    if cantidad <= 0:
                        print("\nError. La cantidad del producto debe ser mayor a 0.")
                    else:
                        break
                except ValueError:
                    print("\nError. La cantidad del producto debe ser un número entero.")

            agregar_producto(nombre, precio, cantidad)

        case 2:
            while True:
                nombre = input("\nIngrese el nombre del producto que desea buscar en el inventario: ").strip().lower()
                if nombre == "":
                    print("\nError. El nombre del producto no puede estar vacío.")
                else:
                    break

            consultar_producto(nombre)

        case 3:
            while True:
                nombre = input("\nIngrese el nombre del producto: ").strip().lower()
                if nombre == "":
                    print("\nError. El nombre del producto no puede estar vacío.")
                else:
                    break

            while True:
                try:
                    precio = input("\nIngrese el precio actualizado del producto: ")
                    precio = float(precio)
                    if precio <= 0:
                        print("\nError. El precio del producto debe ser mayor a 0.")
                    else:
                        break
                except ValueError:
                    print("\nError. El precio del producto debe ser un número.")

            actualizar_precio(nombre, precio)

        case 4:
            while True:
                nombre = input("\nIngrese el nombre del producto que desea eliminar: ").strip().lower()
                if nombre == "":
                    print("\nError. El nombre del producto no puede estar vacío.")
                else:
                    break

            eliminar_producto(nombre)

        case 5:
            print(f"\n{'Nombre':<20} {'Precio':<20} {'Cantidad':<20}")
            print("-" * 60)
            for producto in productos:
                print(f"{producto['Nombre']:<20} {producto['Precio']:<20.2f} {producto['Cantidad']:<20}")

            print(f"\nEl total del costo del inventario es: ${total_del_inventario():.2f}")

        case 6:
            mostrar_inventario()

        case 7:
            print("\nSaliendo del programa. ¡Hasta luego!")
            break

        case _:
            print("\nOpción no válida. Por favor, seleccione una opción del 1 al 7.")
