using System;
using Complex;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;


namespace Complex
{
    public class myDouble
    {
        protected double num;

        //parameterless constructor
        public myDouble() { }

        //constructor with parameter
        public myDouble(double num)
        {
            this.num = num;
        }

        //overloading operator +
        public static myDouble operator +(myDouble first, myDouble second)
        {
            myDouble temp = new myDouble();
            temp.num = first.num + second.num;
            return temp;
        }


        //overloading operator -
        public static myDouble operator -(myDouble first, myDouble second)
        {
            myDouble temp = new myDouble();
            temp.num = first.num - second.num;
            return temp;
        }

        //overloading operator *
        public static myDouble operator *(myDouble first, myDouble second)
        {
            myDouble temp = new myDouble();
            temp.num = first.num * second.num;
            return temp;
        }

        //overloading operator /
        public static myDouble operator /(myDouble first, myDouble second)
        {
            myDouble temp = new myDouble();
            temp.num = first.num / second.num;
            return temp;
        }

        //overloading operator ==
        public static bool operator ==(myDouble first, myDouble second)
        {
            return first.num == second.num;
        }

        //overloading operator !=
        public static bool operator !=(myDouble first, myDouble second)
        {
            return !(first == second);
        }
        
        //overloading operator <
        public static bool operator <(myDouble first, myDouble second)
        {
            return (first.num < second.num);
        }

        //overloading operator >
        public static bool operator >(myDouble first, myDouble second)
        {
            return (first.num > second.num);
        }

        //function for output
        public void write()
        {
            Console.Write(num);
        }

        //converting myDouble to double to use sqrt 
        public double convert()
        {
            return num;
        }
    }

    public class myComplex
    {
        private myDouble re;
        private myDouble im;
        //parameterless constructor
        public myComplex() { }

        //constructor with parameters
        public myComplex(myDouble re, myDouble im)
        {
            this.re = re;
            this.im = im;
        }

        //overloading operator+
        public static myComplex operator +(myComplex first, myComplex second)
        {
            myComplex temp = new myComplex();
            temp.re = first.re + second.re;
            temp.im = first.im + second.im;
            return temp;
        }

        //overloading operator-
        public static myComplex operator -(myComplex first, myComplex second)
        {
            myComplex temp = new myComplex();
            temp.re = first.re - second.re;
            temp.im = first.im - second.im;
            return temp;
        }

        //overloading operator*
        public static myComplex operator *(myComplex first, myComplex second)
        {
            myComplex temp = new myComplex();
            temp.re = first.re * second.re - first.im * second.im;
            temp.im = first.re * second.im + second.re * first.im;
            return temp;
        }

        //magnitude
        public myDouble magnitude()
        {
            myDouble temp = new myDouble((re * re + im * im).convert());
            double ans = Math.Sqrt(temp.convert());
            return new myDouble(ans);
        }

        //overloading operator/
        public static myComplex operator /(myComplex c1, myComplex c2)
        {
            return (new myComplex((c1.re * c2.re + c1.im * c2.im) / (c2.re * c2.re + c2.im * c2.im),
                    (c2.re * c1.im - c1.re * c2.im) / (c2.re * c2.re + c2.im * c2.im)));
        }

        //argument
        public myDouble argument()
        {
            myDouble temp = new myDouble(Math.Atan((im / re).convert()));
            return temp;
        }

        //overloading operator==
        public static bool operator ==(myComplex first, myComplex second)
        {
            return (first.re == second.re && first.im == second.im);
        }

        //overloading operator!=
        public static bool operator !=(myComplex first, myComplex second)
        {
            return !(first == second);
        }

        //output
        public void write()
        {
            myDouble zero = new myDouble(0);
            if (im == zero)
            {
                re.write();
                return;
            }
            if (re == zero)
            {
                im.write();
                return;
            }
            re.write();
            if (im > zero)
                Console.Write("+");
            im.write();
            Console.WriteLine("*i");
        }
    }

}


class Program
{
    static void Main(string[] args)
    {
        myDouble re = new myDouble(3);
        myDouble im = new myDouble(1);
        myComplex a = new myComplex(re, im);
        a.write();
        re = new myDouble(1);
        im = new myDouble(2);
        myComplex b = new myComplex(re, im);
        (a + b).write();
        (a - b).write();
        (a * b).write();
        (a + b).magnitude().write();
        Console.WriteLine();
        (a / b).write();
        (a / b).argument().write();
        Console.WriteLine();
     }
}
