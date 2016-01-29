# Priority_Queue_For_.NET

A simple and super efficient priority Queue for .NET that uses a min heap for the underlying data structure.

## Usage

### Primitive Types

    var queue = new PriorityQueue<int>();
    
    var rando = new Random();
    var max = 10;
    
    for (int i = 0; i < max; i++)
    {
        queue.Offer(rando.Next(max));
    }

    while (queue.Count > 0)
    {
        var next = queue.Poll();
    }

### Complex Objects (Badgers)

#### First, our Badger class

    public class Badger
    {
        public string Color { get; set; }

        public double Weight { get; set; }

        // IMPORTANT: the less than operator must be overloaded to use this object
        // in the priority queue
        
        public static bool operator <(Badger b1, Badger b2)
        {
            return b1.Weight < b2.Weight;
        }
        
        // The greater than operator will not be used in the priority queue, but
        // you must implement both. I recommend the following.
        
        public static bool operator >(Badger b1, Badger b2)
        {
            return !(b1 < b2);
        }
    }

#### Next, Badger prioritizing

    var badgers = new []
    {
        new Badger { Color = "White", Weight = 20.5 },
        new Badger { Color = "Brown", Weight = 53.71 },
        new Badger { Color = "Black", Weight = 16.3 },
    };

    var baderQueue = new PriorityQueue<Badger>();

    foreach (var badger in badgers)
    {
        baderQueue.Offer(badger);
    }

    while (baderQueue.Count > 0)
    {
        var nextBadger = baderQueue.Poll();
        Console.WriteLine("The {0} badger weighs {1} lbs", nextBadger.Color, nextBadger.Weight);
    }

If you run this code you will see the badgers will be printed in the correct order, by weight!

    The Black badger weighs 16.3 lbs
    The White badger weighs 20.5 lbs
    The Brown badger weighs 53.71 lbs