using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Assignement_03
{
    public class Docs
    {
        public string documentName;
        public string documentPath;
        public Docs(string documentName, string documentPath)
        {
            this.documentName = documentName;
            this.documentPath = documentPath;
        }
    }
    public class Applicant
    {
        public string applicantName;
        public string applicantCity;
        public double applicantCGPA;
        public List<Docs> applicantDocs;
        public List<int> applicantsMarks = new List<int>();
        public Applicant(string applicantName, string applicantCity, double applicantCGPA)
        {
            this.applicantName = applicantName;
            this.applicantCity = applicantCity;
            this.applicantCGPA = applicantCGPA;
        }
        public void setApplicantMarks(int marks)
        {
            applicantsMarks.Add(marks);
        }
    }
    internal class Program
    {
        static void Main(string[] args)
        {
            string[] arrayNames = {"Ahmad Hussian", "Muhammad Hassan", "Muhammad Ibrahim", "Shehzad Niaz", "Ali Zaman", "Taimoor Pal", "Usama Iqbal",
                                    "Usman Ahmad", "Waleed Qaiser", "Ibtisam Hassan", "Danish Bismillah", "Aqib Ali", "Adil Latif", "Muhammad Awais",
                                    "Aziz Wahllah"};
            string[] arrayCities = {"Lahore", "Rawalpindi", "Karachi", "Lahore", "Peshawar", "Multan", "Islamabad",
                                    "Rawalpindi", "Lahore", "Quetta", "Quetta", "Kashmir", "Lahore", "Karachi",
                                    "Peshawar"};
            double[] arrayCGPA = { 3.19, 3.1, 3.01, 3.4, 3.45, 2.6, 2.7, 3.0, 2.8, 2.5, 3.5, 3.6, 3.0, 2.9, 3.8 };
            List<Applicant> selectedApplicants = new List<Applicant>();
            List<Applicant> above90Applicants = new List<Applicant>();
            //Dictionary<string, List<string>> candidateDict = new Dictionary<string, List<string>>();
            Dictionary<string,string> candidateDict = new Dictionary<string, string>();
            Console.WriteLine("Selected Applicants Are : \n");
            for (int i = 0; i < arrayNames.Length; i++)
            {
                Applicant applicant = new Applicant(arrayNames[i], arrayCities[i].ToLower(), arrayCGPA[i]);
                if (candidateDict.ContainsKey(applicant.applicantCity))
                {
                    candidateDict[applicant.applicantCity] = candidateDict[applicant.applicantCity] + "\n" + (applicant.applicantName);
                }
                if (!candidateDict.ContainsKey(applicant.applicantCity))
                {
                    candidateDict.Add(applicant.applicantCity, applicant.applicantName);
                }
                if (applicant.applicantCGPA >= 3.0)
                {
                    selectedApplicants.Add(applicant);
                    Console.WriteLine(applicant.applicantName);
                }
            }
            Console.WriteLine("\nSelected Candidates With Marks 90% Or Above Are : \n");
            for (int i = 0; i < selectedApplicants.Count; i++)
            {
                Random random = new Random();
                selectedApplicants[i].setApplicantMarks(random.Next(0, 101));
                selectedApplicants[i].setApplicantMarks(random.Next(0, 101));
                if (Convert.ToDouble(selectedApplicants[i].applicantsMarks.Sum() / 2.0) >= 90.0)
                {
                    Console.WriteLine(selectedApplicants[i].applicantName);
                    above90Applicants.Add(selectedApplicants[i]);
                }
            }
            Console.WriteLine("Enter The City You Want To Search Candidates From : ");
            string cityName = Console.ReadLine();
            Console.WriteLine(candidateDict[cityName.ToLower()]);
            Console.ReadLine();
        }
    }
}
