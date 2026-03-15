![avatar](avatar.jpg)
# Zahar Karapetian

- **Телефон:** +375447726981  
- **Email:** zah4r.karapetian@yandex.ru  
- **Instagram:** zahar_696

## About Me
Студент 2-го курса Белорусско-Российского университета.  
С каждой новой лекцией появляется интерес узнавать что-то новое. Моя цель — получение высшего образования.

## Experience
### Work Experience
- Написание программ на C# с использованием консольных приложений.
- Использование C# в средах разработки, таких как Windows Forms и WPF.

### Пример кода на C#
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Лаб.раб._14_2_задание
{
    struct Student
    {
        public string LastName { get; set; }
        public string Group { get; set; }
        public int ProgrammingGrade { get; set; }
        public int HistoryGrade { get; set; }

        public Student(string lastName, string group, int programmingGrade, int historyGrade)
        {
            LastName = lastName;
            Group = group;
            ProgrammingGrade = programmingGrade;
            HistoryGrade = historyGrade;
        }
    }

    class Program
    {
        static List<(Student, string)> GetStudentsWithLowGrades(List<Student> students)
        {
            var lowGradeStudents = new List<(Student, string)>();

            foreach (var student in students)
            {
                if (student.ProgrammingGrade < 3)
                    lowGradeStudents.Add((student, "Программирование"));
                if (student.HistoryGrade < 3)
                    lowGradeStudents.Add((student, "История"));
            }

            return lowGradeStudents;
        }

        static Dictionary<string, double> CalculateAverageGradesByGroup(List<Student> students)
        {
            return students.GroupBy(s => s.Group)
                        .ToDictionary(g => g.Key, g => g.Average(s => (s.ProgrammingGrade + s.HistoryGrade) / 2.0));
        }

        static List<Student> GetTopStudents(List<Student> students, Dictionary<string, double> groupAverages)
        {
            return students.Where(s =>
                (s.ProgrammingGrade + s.HistoryGrade) / 2.0 > groupAverages[s.Group]).ToList();
        }

        static List<Student> SortStudentsByAverageGrade(List<Student> students)
        {
            return students.OrderBy(s => (s.ProgrammingGrade + s.HistoryGrade) / 2.0).ToList();
        }

        static void DisplayMenu()
        {
            Console.WriteLine("Меню:");
            Console.WriteLine("1. Ввод данных о студентах");
            Console.WriteLine("2. Вывод студентов с двойками");
            Console.WriteLine("3. Средние баллы по группам");
            Console.WriteLine("4. Вывод студентов с баллом выше среднего по группе");
            Console.WriteLine("5. Сортировка студентов по среднему баллу");
            Console.WriteLine("6. Выход");
        }

        static void Main(string[] args)
        {
            List<Student> students = new List<Student>();
            bool exit = false;

            while (!exit)
            {
                DisplayMenu();
                Console.Write("Выберите пункт меню: ");
                int choice = int.Parse(Console.ReadLine());

                switch (choice)
                {
                    case 1:
                        Console.Write("Введите количество студентов: ");
                        int count = int.Parse(Console.ReadLine());

                        for (int i = 0; i < count; i++)
                        {
                            Console.WriteLine($"Студент {i + 1}:");
                            Console.Write("Введите фамилию: ");
                            string lastName = Console.ReadLine();
                            Console.Write("Введите группу: ");
                            string group = Console.ReadLine();
                            Console.Write("Введите оценку по программированию: ");
                            int programmingGrade = int.Parse(Console.ReadLine());
                            Console.Write("Введите оценку по истории: ");
                            int historyGrade = int.Parse(Console.ReadLine());

                            students.Add(new Student(lastName, group, programmingGrade, historyGrade));
                        }

                        break;

                    case 2:
                        var lowGrades = GetStudentsWithLowGrades(students);
                        Console.WriteLine("Студенты с двойками:");
                        foreach (var (student, subject) in lowGrades)
                        {
                            Console.WriteLine($"{student.LastName}, группа {student.Group}, предмет: {subject}");
                        }

                        break;

                    case 3:
                        var groupAverages = CalculateAverageGradesByGroup(students);
                        Console.WriteLine("Средние баллы по группам:");
                        foreach (var kvp in groupAverages)
                        {
                            Console.WriteLine($"Группа {kvp.Key}: {kvp.Value:F2}");
                        }

                        break;

                    case 4:
                        var averages = CalculateAverageGradesByGroup(students);
                        var topStudents = GetTopStudents(students, averages);
                        Console.WriteLine("Студенты с баллом выше среднего по группе:");
                        foreach (var student in topStudents)
                        {
                            Console.WriteLine($"{student.LastName}, группа {student.Group}");
                        }

                        break;

                    case 5:
                        var sortedStudents = SortStudentsByAverageGrade(students);
                        Console.WriteLine("Студенты, отсортированные по среднему баллу:");
                        foreach (var student in sortedStudents)
                        {
                            double avg = (student.ProgrammingGrade + student.HistoryGrade) / 2.0;
                            Console.WriteLine($"{student.LastName}, группа {student.Group}, средний балл: {avg:F2}");
                        }

                        break;

                    case 6:
                        exit = true;
                        break;

                    default:
                        Console.WriteLine("Некорректный ввод, попробуйте снова.");
                        break;
                }
            }
        }
    }
}
```

