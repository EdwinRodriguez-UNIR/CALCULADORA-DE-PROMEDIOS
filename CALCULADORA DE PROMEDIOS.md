def ingresar_calificaciones():
    materias = []
    calificaciones = []
    while True:
        materia = input("Ingrese el nombre de la materia: ")
        while True:
            try:
                calificacion = float(input(f"Ingrese la calificación de {materia} (entre 0 y 10): "))
                if 0 <= calificacion <= 10:
                    break
                else:
                    print("La calificación debe estar entre 0 y 10.")
            except ValueError:
                print("Por favor, ingrese un número válido para la calificación.")
        materias.append(materia)
        calificaciones.append(calificacion)
        continuar = input("¿Desea ingresar otra materia? (s/n): ").lower()
        if continuar != 's':
            break
    return materias, calificaciones
def calcular_promedio(calificaciones):
    if len(calificaciones) == 0:
        return 0
    return sum(calificaciones) / len(calificaciones)
def determinar_estado(calificaciones, umbral=5.0):
    aprobadas = []
    reprobadas = []
    for i, calificacion in enumerate(calificaciones):
        if calificacion >= umbral:
            aprobadas.append(i)
        else:
            reprobadas.append(i)
    return aprobadas, reprobadas
def encontrar_extremos(calificaciones):
    if len(calificaciones) == 0:
        return None, None
    max_index = calificaciones.index(max(calificaciones))
    min_index = calificaciones.index(min(calificaciones))
    return max_index, min_index
def main():
    print("Bienvenido a la Calculadora de Promedios de Calificaciones")
    materias, calificaciones = ingresar_calificaciones()
    if len(materias) == 0:
        print("No se ingresaron materias.")
        return
    promedio = calcular_promedio(calificaciones)
    aprobadas, reprobadas = determinar_estado(calificaciones)
    mejor_index, peor_index = encontrar_extremos(calificaciones)
    print("\nResumen de calificaciones:")
    for i, materia in enumerate(materias):
        print(f"{materia}: {calificaciones[i]}")
    print(f"\nPromedio general: {promedio:.2f}")
    print("\nMaterias aprobadas:")
    for i in aprobadas:
        print(f"- {materias[i]}: {calificaciones[i]}")
    print("\nMaterias reprobadas:")
    for i in reprobadas:
        print(f"- {materias[i]}: {calificaciones[i]}")
    if mejor_index is not None and peor_index is not None:
        print(f"\nMateria con la mejor calificación: {materias[mejor_index]} con {calificaciones[mejor_index]}")
        print(f"Materia con la peor calificación: {materias[peor_index]} con {calificaciones[peor_index]}")
    print("\n¡Gracias por usar la Calculadora de Promedios! Hasta luego.")
if __name__ == "__main__":
    main()
