# mi-proyecto
Una breve descripción del proyecto.
class Cuenta:
    def __init__(self, numero, dni, titular, saldo=0, activa=True):
        self.numero = numero
        self.dni = dni
        self.titular = titular
        self.saldo = saldo
        self.activa = activa

    def __str__(self):
        estado = "Activa" if self.activa else "Inactiva"
        return (f"N° Cuenta: {self.numero}, Titular: {self.titular}, DNI: {self.dni}, "
                f"Saldo: ${self.saldo}, Estado: {estado}")

cuentas = []

def buscar_cuenta(numero):
    for cuenta in cuentas:
        if cuenta.numero == numero:
            return cuenta
    return None
        
def alta_cuenta():
    numero = input("Ingrese numero de cuenta:")
    if buscar_cuenta(numero):
        print("Ya existe una cuenta con ese numero.")
        return
    dni = input("Ingrese el DNI del titular: ")
    titular = input("Ingrese nombre del titular:")
    saldo = float(input("Ingrese saldo inicial:"))
    cuenta = Cuenta(numero, dni, titular, saldo)
    cuentas.append(cuenta)
    print("Cuenta creada exitosamente.")

def depositar():
    numero = input("Ingrese numero de cuenta: ")
    cuenta = buscar_cuenta(numero)
    if cuenta and cuenta.activa:
        monto = float(input("Ingrese monto a depositar: "))
        cuenta.saldo += monto
        print(f"Deposito exitoso. Nuevo saldo: ${cuenta.saldo}")
    elif cuenta:
        print("La cuenta esta inactiva.")
    else:
        print("Cuenta no encontrada.")

def extraer():
    numero = input("Ingrese numero de cuenta:")
    cuenta = buscar_cuenta(numero)
    if cuenta and cuenta.activa:
        monto = float(input("Ingrese monto a extraer:"))
        if monto <= cuenta.saldo:
            cuenta.saldo-=monto
            print(f"Extracion exitosa. Nuevo saldo: ${cuenta.saldo}")
        else:
            print("Fondos insuficientes")
    elif cuenta:
        print("La cuenta esta inactiva")
    else:
        print("Cuenta no encontrada")

def buscar_por_dni_():
    dni = input("Ingrese DNI a buscar:\n")
    encontradas = [c for c in cuentas if c.dni==dni]
    if encontradas:
        for c in encontradas:
            print(c)
    else:
        print("No se encontraron cuentas con ese DNI.")

def activar_cuenta():
    numero=input("Ingrese numero de cuenta:\n")
    cuenta=buscar_cuenta(numero)
    if cuenta:
        cuenta.activa = True
        print("Cuenta activada.")
    else:
        print("Cuenta no encontrada.")

def desactivar_cuenta():
    numero=input("Ingrese numero de cuenta:\n")
    cuenta=buscar_cuenta(numero)
    if cuenta:
        cuenta.activa=False
        print("Cuenta desactivada.")
    else:
        print("Cuenta no encontrada.")

def imprimir_cuentas():
    if cuentas:
        for cuenta in cuentas:
            print(cuenta)
    else:
        print("No hay cuentas registradas.")

def menu():
    while True:
        print("\n--- MENU DE CUENTAS ---")
        print("1. Alta de cuenta")
        print("2. Depositar")
        print("3. Extraer")
        print("4. Busqueda por DNI")
        print("5. Activar cuenta")
        print("6. Desactivar cuenta")
        print("7. Imprimir todas las cuentas")
        print("0. Salir")

        opcion=input("Seleccione una opcion:")

        if opcion == "1":
            alta_cuenta()
        elif opcion == "2":
            depositar()
        elif opcion == "3":
            extraer()
        elif opcion == "4":
            buscar_por_dni_()
        elif opcion == "5":
            activar_cuenta()
        elif opcion == "6":
            desactivar_cuenta()
        elif opcion == "7":
            imprimir_cuentas()
        elif opcion == "0":
            print ("Saliendo el programa...")
            break
        else:
            print("Opcion no valida. Intente nuevamente.")

menu()
