using System;
using System.Collections.Generic;
using System.Text;
using Test;

namespace Test
{
    public interface IPoint
    {
        int X { get; set; }
        int Y { get; set; }
        string ToString();
    }

    public interface IShape
    {
        void Perimeter();
        void Square();
    }

    public class Point : IPoint
    {
        public int X { get; set; }
        public int Y { get; set; }

        public Point(int x, int y)
        {
            X = x;
            Y = y;
        }

        public override string ToString()
        {
            int a = this.X;
            int b = this.Y;
            return this.X + "," + this.Y;
        }
    }
    
    public class Triangle : IPoint, IShape
    {
        public  Point a, b, c;
        public Triangle(Point A, Point B, Point C)
        {
            this.a = A;
            this.b = B;
            this.c = C;

            try
            {
                Point AB = new Point(B.X - A.X, B.Y - A.Y);
                Point BC = new Point(C.X - B.X, C.Y - A.Y);
                double a = AB.X / BC.X;
                double b = AB.Y / BC.Y;
                double c = 1 / (a - b);
            }
            catch(DivideByZeroException)
            {
                Exception exception = new Exception("3 diem khong duoc thang hang");
                throw exception;
            }
        }
        public int X { get => a.X; set => a.X = value; }
        public int Y { get => a.Y; set => a.Y = value; }

        public double Distance(Point A, Point B)
        {
            double C = Math.Sqrt(Math.Pow((B.X - A.X), 2) + Math.Pow((B.Y - A.Y), 2));
            return C;
        }

        public double perimeter()
        {
            return Distance(a , b) + Distance(c, b)+ Distance(a, c);
        }


        public double square()
        {
            double s1 = (b.X - a.X) * (c.Y - a.Y);
            double s2 = (c.X - a.X) * (b.Y - a.Y);
            double s3 = Math.Abs(s1 - s2) / 2;
            return s3;
        }

        public void Perimeter()
        {
            Console.WriteLine("Perimeter:" + perimeter());
        }
        public void Square()
        {
            Console.WriteLine("Square:" + square());
        }
    }


    class Test
    {
        static void Main(string[] args)
        {
            Point A = new Point(2, 3);
            Point B = new Point(3, 3);
            Point C = new Point(4, 5);
            Triangle triangle = new Triangle(A, B, C);
            triangle.Perimeter();
            triangle.Square();
        
        }
    }

}

   

