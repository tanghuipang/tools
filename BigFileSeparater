//a tool for separate big log file into pieces, since it's too difficult to open a text file bigger than 1GB.
using System;
using System.IO;

namespace BigFileSeparater
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Title = "BIG TEXT FILE SEPARATER";
            Console.WriteLine("please enter the file path:");
            string path = Console.ReadLine().Trim();
            if (path.StartsWith("\""))
                path = path.Replace('\"', ' ').Trim();
            while (!File.Exists(path))
            {
                Console.WriteLine("invalid file path, please re-enter:");
                path = Console.ReadLine().Trim();
            }

            StreamReader streamReader = new StreamReader(path);
            string maxLineStr = "";
            Console.WriteLine("please enter max line count of separated file:");
            bool ok = false;
            int maxValue = 65535 * 100;
            int maxLine = 100;
            do
            {
                maxLineStr = Console.ReadLine().Trim();
                ok = int.TryParse(maxLineStr, out maxLine);
                if (!ok)
                {
                    Console.WriteLine("invalid number, please re-enter:");
                }

                if (maxLine > maxValue)
                {
                    Console.WriteLine($"max value is {maxValue}, please enter a smaller value:");
                    ok = false;
                }
            }
            while (!ok);
            long currentPart = 0;
            long lineCount = 0;
            var dir = Path.GetDirectoryName(path);
            var fileName = Path.GetFileNameWithoutExtension(path);
            var ext = Path.GetExtension(path);
            while(!streamReader.EndOfStream)
            {
                string partName = Path.Combine(dir, fileName + currentPart.ToString() + ext);
                using (var sw = File.CreateText(partName))
                {
                    currentPart++;
                    for (int i = 0; i < maxLine; i++)
                    {
                        string line = streamReader.ReadLine();
                        sw.WriteLine(line);
                        lineCount++;
                        if (streamReader.EndOfStream)
                            break;
                    }
                    Console.WriteLine($"write to file:{partName} current total line count:{lineCount}");
                }
            }

            Console.WriteLine("separete finished. print any key to continue.");
            Console.ReadKey();
        }
    }
}
