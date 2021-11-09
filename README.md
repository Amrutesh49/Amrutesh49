using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace IPLApplication
{
    class Team
    {
        String teamName;
        String country;

        public Team()
        {
        }

        public Team(string teamName, string country)
        {
            TeamName = teamName;
            Country = country;
        }

        public string TeamName { get => teamName; set => teamName = value; }
        public string Country { get => country; set => country = value; }

        public override string ToString()
        {
            return String.Format("Team Name : {0}  Country : {1}", teamName, country);
        }
        public override bool Equals(object obj)
        {
            Team t = (Team)obj;
            return this.teamName == t.teamName && this.Country == t.Country;
        }
        public override int GetHashCode()
        {
            return base.GetHashCode();
        }
    }
}





using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace IPLApplication
{
    class Players : Team,IComparable
    {
        int id;
        String Name;
        int age;
        String Batting_Style;
        String Bowling_Style;

        public Players()
        {
        }

        public Players(string teamName, string country ,int id, string name1, int age, string batting_Style1, string bowling_Style1 )
        {
            TeamName = TeamName;
            Country = Country;
            Id = id;
            Name1 = name1;
            Age = age;
            Batting_Style1 = batting_Style1;
            Bowling_Style1 = bowling_Style1;
        }

        public int Id { get => id; set => id = value; }
        public string Name1 { get => Name; set => Name = value; }
        public int Age { get => age; set => age = value; }
        public string Batting_Style1 { get => Batting_Style; set => Batting_Style = value; }
        public string Bowling_Style1 { get => Bowling_Style; set => Bowling_Style = value; }

        public override string ToString()
        {
            return String.Format("TeamName : {0} \n Country : {1}  \n Id : {2} \n Name : {3} \n Age : {4} \n  Batting Style : {5} \n BowlingStyle  : {6}",TeamName,Country, id, Name, age, Batting_Style, Bowling_Style); 
        }
        public override bool Equals(object obj)
        {
            Players t = (Players)obj;
            return this.Name.Equals( t.Name) && this.TeamName.Equals(t.TeamName);
        }
        public override int GetHashCode()
        {
            return base.GetHashCode();
        }

        public int CompareTo(object obj)
        {
            Players t = (Players)obj;
            return this.id.CompareTo(t.id);
        }
    }
}





using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace IPLApplication
{
    class SortByTeamName : IComparer<Players>
    {
        public int Compare(Players x, Players y)
        {
            return x.Name1.CompareTo(y.Name1);
        }
    }
}




using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace IPLApplication
{
    class SortDesPlayer : IComparer<Players>
    {
        public int Compare(Players x, Players y)
        {
            return x.Batting_Style1.CompareTo(y.Batting_Style1);
        }
    }
}




using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace IPLApplication
{
    class PlayersBO : Players
    {
       public Players[] searchByTeamName(Players[] playerlist )
        {
            SortByTeamName ascSortbyteam = new SortByTeamName();
            Array.Sort(playerlist, ascSortbyteam);
            return playerlist;
        }
        public Players[] searchByBattingStyle(Players[] playerlist)
        {
            SortDesPlayer desSort = new SortDesPlayer();
            Array.Sort(playerlist, desSort);
            return playerlist;
        }
    }
}






using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace IPLApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            Players[] playerDetails = null;
            Console.WriteLine("Enter the no of players");
            int no = Convert.ToInt32(Console.ReadLine());
            Players[] p = new Players[no];
            for(int i=0;i<no; i++)
            {
                p[i] = new Players();
                Console.WriteLine("Enter the Team_Name :");
                p[i].TeamName = Console.ReadLine();
                Console.WriteLine("Enter the Country :");
                p[i].Country = Console.ReadLine();
                Console.WriteLine("Enter the Id :");
                p[i].Id =Convert.ToInt32( Console.ReadLine());
                Console.WriteLine("Enter the Name :");
                p[i].Name1 = Console.ReadLine();
                Console.WriteLine("Enter the age :");
                p[i].Age =Convert.ToInt32( Console.ReadLine());
                Console.WriteLine("Enter the Batting_Style :");
                p[i].Batting_Style1 = Console.ReadLine();
                Console.WriteLine("Enter the Bowling_Style :");
                p[i].Bowling_Style1= Console.ReadLine();
                Console.WriteLine("Thank you Entering player Details");
            }
            

            Console.WriteLine("Plsyers Sorted List  are :");
            Console.WriteLine("1.Sort By PlayersName");
            Console.WriteLine("2.Sort By Players BattingStyle");
            Console.WriteLine("Enter your choice");
            int ch = Convert.ToInt32(Console.ReadLine());
            PlayersBO Player = new PlayersBO();
            Players[] SortedPlayerDetails = null;
            switch(ch)
            {
                case 1:
                    {
                        SortedPlayerDetails = Player.searchByTeamName(playerDetails);
                        break;
                    }
                case 2:
                    {
                        SortedPlayerDetails = Player.searchByBattingStyle(playerDetails);
                        break;
                    }
                default:
                    {
                        Console.WriteLine("Please enter a Correct Option...!");
                        Console.WriteLine("Thank you");
                        break;
                    }
                    if(SortedPlayerDetails!=null)
                    {
                        foreach (var item in SortedPlayerDetails)
                        {
                            Console.WriteLine(item);
                        }
                    }
            }

        }
    }
}

