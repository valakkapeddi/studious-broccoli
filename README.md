## Java Object-Oriented Programming Crash Course
This is a quick crash-course in the foundations of object-oriented programming in Java, created to augment my cousins' academic training in computer science.  This assumes you've already learned about classes in the rushed, sort of haphazard, and largely useless way that I remember from college. :-)

So first of all, it is incorrect to think of OOP as a programming language feature. OOP isn't the same a classes or overloaded functions or any of that.  OOP is a set of ideas, and a way of thinking about problems and building solutions.  There are programming language features in Java that *support* OOP.  We will try and master OOP by first understanding what these features are, and then seeing how you can use them to write object-oriented code.

***Note:*** This may or may not be the way you were originally taught OOP, and if you see something that looks wrong or different from what you know, don't worry about it.  Sometimes it helps to "approximately" learn something "sort of" accurate, use that to build a foundation of knowledge, and then refine your understand to be fully correct later.


- [Part 1: Encapsulation](#solving-problems-by-breaking-them-into-smaller-pieces)
  - [Hints for how to use encapsulation to simplify your design.](#hints-for-how-to-use-encapsulation-to-simplify-your-design)
  - [Assignment for Part 1](#assignment-for-part-1)


#### Solving problems by breaking them into smaller pieces
One of the first things we learn in programming is the concept of __scope__. For instance, variables are contained inside the scope of the function where they are defined - we call these _local_ variables.

Classes also create scopes. Variables & functions defined in a class are visible to all other functions defined in that class (functions defined inside a class are called **methods**).  Whether, and how, any of these are visible *outside* the class, is determined in Java by visibility modifiers - public, private, and so on.

Turns out we can use this to write classes that divide a large problem into smaller pieces, and hide everything about that small bit of the problem except whatever is needed to make it work with the other small bits.  This idea is called ***information hiding*** or ***encapsulation***.

For instance, think about a car's internal combustion engine works. The engine runs by taking fuel into its cylinders, mixing it with air, using spark plugs to ignite this mixture, and uses the resulting reaction to turn the crankshaft. The transmission carries the spinning motion to your wheels, and your car moves.

In that example, the only parts of the engine that the rest of the car needs to worry about are the crankshaft, and the fuel line.  Therefore, we can use encapsulation to take the rest of the engine parts - cylinders, spark plugs, etc - and sink them into the engine block. Think about how much easier this makes it to build a car; we can assemble the engine by itself, make sure it works, and then put it together with the rest of the car, and it should just work.

###### Hints for how to use encapsulation to simplify your design
 - Before you begin to break down the problem, you have to understand the problem. Ask yourself: who is trying to use the system, what are they trying to do, and why? Come up with a story - first, at a high level.
 - Look for 'nouns' in your story.  For instance, in a system that delivers mail, your nouns will be the mail, mailboxes, a postal officer, a post office, and a mail van.
 - Once you have that, determine how these nouns interact with each other.  For instance, you know that mail (for the delivery story anyway) starts out at the post office.  Then, the letter is loaded on to a mail van. Once the post officer reaches the right mailbox, they will take the letter out of the van, carry it to the mailbox, and deliver it.  So the letter interacts with the post office, mail van, post officer, and the mailbox. The truck interacts with the post office where it is loaded, and with the officer who drivers it.
 - In programming, objects interact with each other by calling methods on them, or being passed as parameters to methods in other objects.  Figure out which way makes sense for a particular interaction.  For instance, the process of loading a letter into a mail van might work like this:

```java
class MailVan {
  private ArrayList<Letters> letters = new ArrayList<>();

  // Note: MailVan interacts with a letter by defining a method which takes
  // Letter as a parameter.
  public void load(Letter letterIn) {
    letters.add(letterIn);  
  }
}

class PostOffice {
  private List<Letters> getLettersForZip(String zipCode) {
    // magic! pretend this works
  }

  // Pretend each mail van is going to a certain zip code.
  // So, we'll load all letters for that zip into the van that delivers there.
  // Note: The PostOffice object interacts with MailVan by defining a method that
  // takes a MailVan as a parameter.
  public void loadVan(MailVan mailVanIn) {
    List<Letters> lettersForZip = getLettersForZip(mailVanIn.zipCode());

    for(Letter letter : lettersForZip) {
      mailVanIn.loadVan(letter);
    }
  }

}
```

##### Assignments for Part 1
1. Complete my design of an object-oriented description of mail delivery.  Assume the mail starts out as letters at a post office, gets picked up by trucks (which are driven by postal officers), and gets delivered at a mailbox. The code doesn't actually have to compile or do anything - the important thing is that you correctly identify the objects and how they interfact, and that responsibilities are properly encapsulated.
2. From scratch, create an object-oriented description of a coffee shop. The code doesn't actually have to compile or do anything - the important thing is that you correctly identify the objects and how they interfact, and that responsibilities are properly encapsulated.
