using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp1
{
    class Student
    {
      


    
        public int IndexNumber;
        public string Name;
        public double GPA;
        public int AdmissionYear;
        public string NIC;
        public Student Next;

        public Student(int index, string name, double gpa, int year, string nic)
        {
            IndexNumber = index;
            Name = name;
            GPA = gpa;
            AdmissionYear = year;
            NIC = nic;
            Next = null;
        }
    }

    class StudentList
    {
        private Student head;

        public void Insert(Student newStudent)
        {
            if (Search(newStudent.IndexNumber) != null)
            {
                Console.WriteLine("Index number must be unique.");
                return;
            }

            if (head == null || newStudent.IndexNumber < head.IndexNumber)
            {
                newStudent.Next = head;
                head = newStudent;
            }
            else
            {
                Student current = head;
                while (current.Next != null && current.Next.IndexNumber < newStudent.IndexNumber)
                    current = current.Next;

                newStudent.Next = current.Next;
                current.Next = newStudent;
            }
        }

        public Student Search(int index)
        {
            Student current = head;
            while (current != null)
            {
                if (current.IndexNumber == index)
                    return current;
                current = current.Next;
            }
            return null;
        }

        public void Remove(int index)
        {
            if (head == null)
            {
                Console.WriteLine("List is empty.");
                return;
            }

            if (head.IndexNumber == index)
            {
                head = head.Next;
                Console.WriteLine("Student removed.");
                return;
            }

            Student current = head;
            while (current.Next != null && current.Next.IndexNumber != index)
                current = current.Next;

            if (current.Next == null)
                Console.WriteLine("Student not found.");
            else
            {
                current.Next = current.Next.Next;
                Console.WriteLine("Student removed.");
            }
        }

        public void PrintAll()
        {
            Student current = head;
            if (current == null)
            {
                Console.WriteLine("No students to display.");
                return;
            }

            while (current != null)
            {
                Console.WriteLine($"Index: {current.IndexNumber}, Name: {current.Name}, GPA: {current.GPA}, Year: {current.AdmissionYear}, NIC: {current.NIC}");
                current = current.Next;
            }
        }
    }

    class Program
    {
        static void Main()
        {
            StudentList list = new StudentList();
            while (true)
            {
                Console.WriteLine("\n1. Insert\n2. Search\n3. Remove\n4. Print All\n5. Exit");
                Console.Write("Choose option: ");
                int option = int.Parse(Console.ReadLine());

                switch (option)
                {
                    case 1:
                        Console.Write("Enter Index Number: ");
                        int index = int.Parse(Console.ReadLine());
                        Console.Write("Enter Name: ");
                        string name = Console.ReadLine();
                        Console.Write("Enter GPA: ");
                        double gpa = double.Parse(Console.ReadLine());
                        Console.Write("Enter Admission Year: ");
                        int year = int.Parse(Console.ReadLine());
                        Console.Write("Enter NIC: ");
                        string nic = Console.ReadLine();
                        list.Insert(new Student(index, name, gpa, year, nic));
                        break;

                    case 2:
                        Student found = list.Search(searchIndex);
                        if (found != null)
                            Console.WriteLine("Found: {found.Name}, GPA: {found.GPA}, Year: {found.AdmissionYear}, NIC: {found.NIC}");
                        else
                            Console.WriteLine("Student not found.");
                        break;

                    case 3:
                        Console.Write("Enter Index Number to remove: ");
                        int removeIndex = int.Parse(Console.ReadLine());
                        list.Remove(removeIndex);
                        break;

                    case 4:
                        list.PrintAll();
                        break;

                    case 5:
                        return;

                    default:
                        Console.WriteLine("Invalid option.");
                        break;
                }
            }
        }
    }
