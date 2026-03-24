using System;

public class Libro
{
    public string Titulo { get; set; }
    public string Autor { get; set; }
    public string Genero { get; set; }
    public int AnioPublicacion { get; set; }
    public int NumeroPaginas { get; set; }

    // Método para registrar un libro
    public void Registrar()
    {
        Console.Write("Ingrese título: ");
        Titulo = Console.ReadLine();

        Console.Write("Ingrese autor: ");
        Autor = Console.ReadLine();

        Console.Write("Ingrese género: ");
        Genero = Console.ReadLine();

        Console.Write("Ingrese año de publicación: ");
        AnioPublicacion = int.Parse(Console.ReadLine());

        Console.Write("Ingrese número de páginas: ");
        NumeroPaginas = int.Parse(Console.ReadLine());

        Console.WriteLine("📚 Libro registrado correctamente.");
    }

    // Método para mostrar libro
    public void Mostrar()
    {
        Console.WriteLine($"Título: {Titulo} | Autor: {Autor} | Año: {AnioPublicacion}");
    }
}

class Program
{
    static void Main(string[] args)
    {
        List<Libro> listaLibros = new List<Libro>();
        bool salir = false;

        while (!salir)
        {
            Console.Clear();
            Console.WriteLine("===== MENÚ =====");
            Console.WriteLine("1. Registrar libro");
            Console.WriteLine("2. Buscar libro");
            Console.WriteLine("3. Mostrar libros");
            Console.WriteLine("4. Salir");
            Console.Write("Seleccione una opción: ");

            int opcion = int.Parse(Console.ReadLine());

            switch (opcion)
            {
                case 1:
                    RegistrarLibro(listaLibros);
                    break;

                case 2:
                    BuscarLibro(listaLibros);
                    break;

                case 3:
                    MostrarLibros(listaLibros);
                    break;

                case 4:
                    salir = true;
                    Console.WriteLine("Saliendo del programa...");
                    break;

                default:
                    Console.WriteLine("Opción inválida.");
                    break;
            }
        }
    }

    static void RegistrarLibro(List<Libro> lista)
    {
        bool continuar = true;

        while (continuar)
        {
            Libro nuevo = new Libro();
            nuevo.Registrar();
            lista.Add(nuevo);

            Console.Write("¿Desea registrar otro libro? (s/n): ");
            continuar = Console.ReadLine().ToLower() == "s";
        }
    }

    static void BuscarLibro(List<Libro> lista)
    {
        bool continuar = true;

        while (continuar)
        {
            Console.Write("Ingrese el título a buscar: ");
            string titulo = Console.ReadLine();

            Libro encontrado = lista.Find(l => l.Titulo.ToLower() == titulo.ToLower());

            if (encontrado != null)
            {
                encontrado.Mostrar();
            }
            else
            {
                Console.WriteLine("❌ El libro no está disponible.");
            }

            Console.Write("¿Desea buscar otro libro? (s/n): ");
            continuar = Console.ReadLine().ToLower() == "s";
        }
    }

    static void MostrarLibros(List<Libro> lista)
    {
        if (lista.Count == 0)
        {
            Console.WriteLine("No hay libros registrados.");
        }
        else
        {
            Console.WriteLine("📚 Lista de libros:");
            foreach (Libro libro in lista)
            {
                libro.Mostrar();
            }
        }

        Console.WriteLine("Presione una tecla para volver al menú...");
        Console.ReadKey();
    }
}
