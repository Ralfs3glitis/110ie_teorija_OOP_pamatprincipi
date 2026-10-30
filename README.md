# Ievads objektorientētajā programmēšanā (OOP) ar C#

_Mācību materiāls par metodēm, objektiem un četriem OOP pamatprincipiem_

## 1. Kapēc OOPojam
Ja programma kļūst **lielāka**, rodas problēma: **dati un darbības ar tiem ir izmētāti dažādās vietās**. 
>[!Piemērs]
>Ja ir 20 mainīgie par lietotāju (vārds, uzvārds, vecums, e-pasts...) un 15 metodes, kas ar tiem strādā, ļoti viegli kaut ko sajaukt vai nejauši sabojāt.

Objektorientētā programmēšanā iespējams **savienot datus un darbības, kas ar tiem saistītas, vienā veselā _objektā_.**

## 2. Kas ir OOP un OOM?

**OOP (Object-Oriented Programming) - objektorientētā programmēšana** ir programmēšanas paradigma (pieeja), kurā programma tiek veidota kā **objektu kopums**, kas savstarpēji sadarbojas. Katrs objekts:

- **zina kaut ko** par sevi (tā _dati_ jeb _stāvoklis_),
- **māk kaut ko darīt** (tā _uzvedība_ jeb _metodes_).

**OOM (Object-Oriented Modeling) - objektorientētā modelēšana** ir process, kas notiek _pirms_ programmēšanas: mēs paskatāmies uz reālo problēmu un uzdodam pāris jautājumus:

1. Kādas "lietas" šajā problēmā ir? (Students, Kurss, Pasniedzējs...)
2. Ko katra no tām _zina_? (Students zina savu vārdu, kursu...)
3. Ko katra no tām _dara_? (Students var pieteikties kursam...)
4. Kā šīs lietas savstarpēji saistītas?

>[!Saīsināti] 
>OOM - izdomājam, kādi objekti vajadzīgi; 
>OOP - tos uzrakstām kodā.**

> **Padoms modelēšanai:** lietvārdi uzdevuma aprakstā bieži kļūst par **klasēm vai īpašībām**, bet darbības vārdi - par **metodēm**.

## 3. Klase un objekts C# valodā

Tie ir divi svarīgākie jēdzieni, un tos bieži jauc.

- **Klase (class)** - _shēma, projekts, šablons, recepte_. Tā apraksta, kādi dati un darbības būs kādam objektu veidam.
- **Objekts (object)** - _konkrēts eksemplārs_, veidots pēc klases šablona. To sauc arī par klases **instanci**.

>[!Piemērs]
klase ir **kūkas recepte**, objekti ir **konkrētas izceptas kūkas**. No vienas receptes var izcept simts kūkas, un katrai var būt cits garšas pildījums, bet visām ir vienāda struktūra.

### Klase `Stundents`

```csharp
class Students
{
    // Lauki (fields) - dati, ko objekts glabā
    public string vards;
    public int vecums;

    // Metode - darbība, ko objekts var veikt
    public void Iepazities()
    {
        Console.WriteLine($"Sveiki! Es esmu {vards}, man ir {vecums} gadi.");
    }
}
```

Objektu izveido ar atslēgvārdu **`new`**:

```csharp
Students s1 = new Students();
s1.vards = "Anna";
s1.vecums = 19;

Students s2 = new Students();
s2.vards = "Jānis";
s2.vecums = 21;

s1.Iepazities(); // Sveiki! Es esmu Anna, man ir 19 gadi.
s2.Iepazities(); // Sveiki! Es esmu Jānis, man ir 21 gadi.
```

Pievērsiet uzmanību: abi objekti ir veidoti no vienas klases, bet katram ir **savi dati**. Metode `Introduce()` katram objektam izdrukā _tieši tā objekta_ datus.

Punkts (`.`) nozīmē: "ej uz šo objektu un izmanto tā datus vai metodi".

### Objekta daļas C# valodā

| Daļa                           | Kas tas ir                                          | Piemērs                           |
| ------------------------------ | --------------------------------------------------- | --------------------------------- |
| **Lauks (field)**              | mainīgais, kas pieder objektam                      | `public int vecums;`              |
| **Īpašība (property)**         | "gudrāks lauks" ar kontroli pār lasīšanu/rakstīšanu | `public int vecums { get; set; }` |
| **Metode (method)**            | darbība, ko objekts var veikt                       | `public void Iepazities()`        |
| **Konstruktors (constructor)** | īpaša metode objekta izveidei                       | `public Students(string vards)`   |

## 4. Objektu metodēs

Ievadā jūs rakstījāt metodes šādi:

```csharp
static void PrintStudent(string vards, int vecums)
{
    Console.WriteLine($"{vards}, {vecums}");
}

PrintStudent("Anna", 19);
```

Šeit metode ir **atsevišķa no datiem** - mums katru reizi jānodod visi dati kā **parametri**.

Objektorientētajā pieejā metode **pieder objektam** un jau "zina" tā datus:

```csharp
s1.Iepazities();   
// nekādi parametri nav vajadzīgi - objekts pats zina savu vārdu un vecumu. 
//Gan metode, gan dati pieder objektam s1.
```

**Salīdzinājums:**

| Statiskā metode                             | Objekta metode                          |
| ------------------------------------------- | --------------------------------------- |
| Ir `static`, pieder pašai klasei/programmai | Nav `static`, pieder konkrētam objektam |
| Izsauc: `Metode()`                          | Izsauc: `objekts.Metode()`              |
| Visi dati jānodod kā parametri              | Metode izmanto paša objekta datus       |

### Metodes kā objekta **spējas** jeb **uzvedība**

Vienkāršākais veids, kā to saprast: **objektam ir divu veidu "īpašības"**:

>[!Kas objekts ir / kas tam ir]
Lauki un īpašības (_atribūti_): krāsa, vārds, ātrums.

>[!Ko objekts var darīt]
Metodes (_spējas jeb uzvedība_): braukt, izdrukāt, aprēķināt.

**Piemērs** ar mašīnu:

```csharp
class Car //klase Mašīna
{
    // atribūts - kāda ir
    public string Color;   
    // atribūts - cik ātri brauc
    public int Speed;
    
    // uzvedība - ko var darīt
    public void Accelerate() // metode Paātrināties
    {
        Speed += 10; 
        // Tā pat, kā rakstīt Speed = Speed + 10
    }

    public void Brake() // metode Bremzēt
    {
        Speed = 0;
    }
}
```

Metodes **maina objekta stāvokli** (`Accelerate` izmaina `Speed`) vai **atgriež informāciju** par to. Tās ir objekta "pogas" - to, ko ārpasaule var pieprasīt objektam izdarīt.

```csharp
Car car = new Car();
car.Color = "Sarkana";
car.Accelerate();
car.Accelerate();
Console.WriteLine(car.Speed); // 20
```

Metodēm objektos var būt arī parametri un atgriežamā vērtība:

```csharp
public bool IsAdult()
{
    return Age >= 18; 
    // True, ja vecums vienāds vai lielāks par 18, 
    // False, ja mazāks
}
```

## 5. Konstruktori

Iepriekš mēs objektu izveidojām un tad lauku pa laukam piešķīrām vērtības. Tas ir neērti, un var aizmirst kaut ko aizpildīt. **Konstruktors** ir īpaša metode, kas **tiek izsaukta automātiski brīdī, kad tiek izveidots objekts** (`new`), un parasti uzstāda sākotnējos datus.

Konstruktora īpatnības:

- nosaukums **sakrīt ar klases nosaukumu**,
- **nav atgriežamā tipa** (pat ne `void`),
- izsaucas tikai ar `new`.

```csharp
class Student
{
    public string Name;
    public int Age;

    // Konstruktors
    public Student(string name, int age)
    {
        Name = name;
        Age = age;
    }

    public void Introduce()
    {
        Console.WriteLine($"Sveiki! Es esmu {Name}, man ir {Age} gadi.");
    }
}

// Lietošana - viss vienā rindā:
Student s = new Student("Anna", 19);
s.Introduce();
```

Tagad **nav iespējams izveidot studentu bez vārda un vecuma** - konstruktors to pieprasa.

### Vairāki konstruktori (pārslogošana)

Vienai klasei var būt vairāki konstruktori ar dažādiem parametriem:

```csharp
public Student(string name, int age)
{
    Name = name;
    Age = age;
}

public Student(string name) : this(name, 18)   // izsauc iepriekšējo konstruktoru
{
}
```

`this` nozīmē "šis pats objekts". Šeit `: this(name, 18)` pasaka: "izmanto otru konstruktoru, vecumam ieliekot 18".

### Noklusējuma konstruktors

Ja klasei **nav neviena konstruktora**, C# pats izveido tukšu (bez parametriem). Tāpēc agrāk `new Student()` darbojās. Tiklīdz jūs uzrakstāt savu konstruktoru ar parametriem, **tukšais vairs netiek veidots automātiski**.

### Ko ievietot konstruktorā?

- Sākotnējo lauku vērtību uzstādīšanu.
- Vērtību pārbaudi (piemēram, vai vecums nav negatīvs).

## 6. Četri OOP pamatprincipi

OOP balstās uz četriem principiem. Viegli atcerēties: **K-M-P-A** (Kapsulēšana, Mantošana, Polimorfisms, Abstrakcija).

---

### 6.1. Kapsulēšana (Encapsulation)

**Ideja:** objekta iekšējie dati un detaļas tiek **paslēptas**, un ārpasaulei tiek dota tikai **kontrolēta piekļuve** caur noteiktām metodēm vai īpašībām.

>[!Dzīves piemērs - kafijas automāts]
Jūs redzat pogas: "Espresso", "Kapučīno", "Atcelt". Jūs varat tās spiest. Bet jums **nav piekļuves** ūdens spiedienam, sūkņa darbībai, temperatūras sensoram vai pupiņu daudzumam. Ja jūs varētu paši griezt ūdens spiedienu, automāts var saplīst.

Automāta ražotājs rūpējas, lai neviens nevarētu radīt bīstamu stāvokli. Tāpat ar objektiem: **klase pati sargā savu datu pareizību.**

**Ko tas dod:**

- **Drošību** - nevar ierakstīt nepareizus datus (piemēram, negatīvu atlikumu).
- **Vieglāku izmaiņu veikšanu** - iekšējo darbību var pārrakstīt, ja "pogas" paliek tādas pašas.
- **Mazāk kļūdu** - mazāk vietu, kur kaut ko var sabojāt.

**Piekļuves modifikatori C# valodā:**

| Modifikators | Nozīme                                           |
| ------------ | ------------------------------------------------ |
| `public`     | pieejams visiem ("pogas")                        |
| `private`    | pieejams tikai pašā klasē ("iekšējie mehānismi") |
| `protected`  | pieejams klasē un mantotājās klasēs              |

**Piemērs C#: kafijas automāts**

```csharp
class CoffeeMachine
{
    // PRIVĀTI dati - ārpasaule tiem nevar piekļūt
    private int _waterPressure = 9;
    private int _beansGrams = 200;

    // PUBLISKAS "pogas"
    public void MakeEspresso()
    {
        if (_beansGrams < 10)
        {
            Console.WriteLine("Pupiņas beigušās!");
            return;
        }

        HeatWater();                 // iekšēja darbība, ko lietotājs neredz
        _beansGrams -= 10;
        Console.WriteLine("Espresso gatavs!");
    }

    // PRIVĀTA metode - iekšēja darbība
    private void HeatWater()
    {
        Console.WriteLine($"Karsējam ūdeni ar spiedienu {_waterPressure} bar...");
    }
}
```

```csharp
CoffeeMachine machine = new CoffeeMachine();
machine.MakeEspresso();          // ✅ strādā

// machine._waterPressure = 100; // ❌ kļūda: lauks ir private
// machine.HeatWater();          // ❌ kļūda: metode ir private
```

Bez kapsulēšanas jebkurš kods varētu uzrakstīt `account.Balance = -1000000;`. Ar kapsulēšanu atlikumu var mainīt **tikai caur metodēm, kas pārbauda noteikumus**.

>[!Atceries]
> Lauki parasti ir `private`, piekļuve - caur `public` metodēm vai īpašībām.

---

### 6.2. Mantošana (Inheritance)

**Ideja:** jauna klase (**atvasinātā klase jeb apakšklase**, _child_) var **pārņemt** citas klases (**bāzes klases**, _parent_) laukus un metodes, un pievienot savus vai mainīt esošos.

>[!Dzīves piemērs: transportlīdzekļi]
Visiem transportlīdzekļiem ir kaut kas kopīgs: marka, spēja sākt braukt un apstāties. Bet automašīnai papildus ir durvis un bagāžnieks, bet velosipēdam - pedāļi un zvaniņš. Mēs neaprakstām "marku" un "braukšanu" katram atsevišķi - mēs to aprakstām **vienreiz** vispārīgā klasē "Transportlīdzeklis", bet īpašās lietas pievienojam konkrētajos veidos.

>[!Piemērs 2]
Bērns manto no vecākiem acu krāsu un dažas rakstura īpašības, bet vienlaikus ir arī savs cilvēks ar savām.

>[!Mantošanas sakarība - "IR"]
Automašīna **IR** transportlīdzeklis ✅
Velosipēds **IR** transportlīdzeklis ✅
Automašīna **IR** durvis ❌ (tā _satur_ durvis, tā ir cita sakarība)

>**Sniegumi:** koda atkārtota izmantošana, loģiska hierarhija, vieglāka uzturēšana.

**Piemērs C#:**

```csharp
// Bāzes klase
class Vehicle
{
    public string Brand;
    public int Speed;

    public Vehicle(string brand)
    {
        Brand = brand;
    }

    public void Start()
    {
        Console.WriteLine($"{Brand} sāk kustību.");
    }

    public void Stop()
    {
        Speed = 0;
        Console.WriteLine($"{Brand} apstājās.");
    }
}

// Atvasinātā klase - ar ':' norāda, ka mantojam no Vehicle
class Car : Vehicle
{
    public int Doors;

    // 'base' izsauc bāzes klases konstruktoru
    public Car(string brand, int doors) : base(brand)
    {
        Doors = doors;
    }

    public void OpenTrunk()
    {
        Console.WriteLine("Bagāžnieks atvērts.");
    }
}

class Bicycle : Vehicle
{
    public Bicycle(string brand) : base(brand) { }

    public void RingBell()
    {
        Console.WriteLine("Ding-ding!");
    }
}
```

```csharp
Car car = new Car("Toyota", 4);
car.Start();        // mantota metode no Vehicle
car.OpenTrunk();    // pašas Car metode

Bicycle bike = new Bicycle("Giant");
bike.Start();       // arī mantota metode
bike.RingBell();
```

**Svarīgi:**

- C# klase var mantot **tikai no vienas** klases.
- `private` lauki **nav pieejami** mantotājā klasē; ja vajag, lieto `protected`.
- Mantošanu lieto tikai tad, ja patiešām ir "IR" sakarība, nevis tikai lai "ietaupītu kodu".

---

### 6.3. Polimorfisms (Polymorphism)

**Ideja:** (grieķu val. "daudz formu") - **viena un tā pati darbība dažādiem objektiem var izpausties atšķirīgi.** Mēs izsaucam vienu un to pašu metodi, bet _kas tieši notiks_, atkarīgs no objekta veida.

>[!Dzīves piemērs: Balsi!]
Ja jūs klasē sakāt "Dzīvnieki, balsi!", suns teiks "Vau!", kaķis - "Miau!", govs - "Mū!". Komanda ir viena, bet katrs dzīvnieks to izpilda pa savam.

>[!Vēl viens piemērs: maksāšanas poga]
>interneta veikalā. Jūs spiežat vienu pogu "Maksāt", bet kartes maksājums, bankas pārskaitījums un Apple Pay notiek pilnīgi atšķirīgi "aizkulisēs".

>**Sniegumi:** varam rakstīt kodu, kas strādā ar "vispārīgu" tipu, un nav jāzina, kāds konkrēti objekts tur atrodas. Jaunus veidus var pievienot, nemainot esošo kodu.

**Piemērs C#:**

Bāzes klasē metodi atzīmējam ar **`virtual`** ("drīkst pārrakstīt"), atvasinātajās - ar **`override`** ("pārrakstu").

```csharp
class Animal
{
    public string Name;

    public Animal(string name)
    {
        Name = name;
    }

    public virtual void MakeSound()
    {
        Console.WriteLine("...kaut kāda skaņa");
    }
}

class Dog : Animal
{
    public Dog(string name) : base(name) { }

    public override void MakeSound()
    {
        Console.WriteLine($"{Name} saka: Vau!");
    }
}

class Cat : Animal
{
    public Cat(string name) : base(name) { }

    public override void MakeSound()
    {
        Console.WriteLine($"{Name} saka: Miau!");
    }
}

class Cow : Animal
{
    public Cow(string name) : base(name) { }

    public override void MakeSound()
    {
        Console.WriteLine($"{Name} saka: Mū!");
    }
}
```

**Polimorfisms noder tagad šeit!**

```csharp
List<Animal> animals = new List<Animal>
{
    new Dog("Reksis"),
    new Cat("Pīlādzis"),
    new Cow("Margrieta")
};

foreach (Animal a in animals)
{
    a.MakeSound();   // viena un tā pati komanda!
}
```

**Rezultāts:**

```
Reksis saka: Vau!
Pīlādzis saka: Miau!
Margrieta saka: Mū!
```

Cikls neko nezina par suņiem vai govīm - tas zina tikai, ka katrs ir `Animal` un māk `MakeSound()`. Ja vēlāk pievienosim `Duck`, cikla kodu nevajadzēs mainīt.

> **Atcerieties:** `virtual` bāzes klasē + `override` atvasinātajā klasē = polimorfisms.

---

### 6.4. Abstrakcija (Abstraction)

**Ideja:** parādīt tikai **būtisko**, bet paslēpt **sarežģītās detaļas**. Mēs definējam, _ko_ objekts dara, nenorādot (vai neuztraucoties), _kā_ tieši.

>[!Dzīves piemērs: Automašīnas vadība]
Vadot auto, jums ir stūre, pedāļi un ātrumkārba. Jūs nezināt (un jums nevajag zināt), kā darbojas iekšdedzes dzinējs, degvielas iesmidzināšana vai bremžu hidraulika. Jums ir vienkāršs **interfeiss** sarežģītai sistēmai.

>[!Cits piemērs: Televizora tālvadības pults]
>Jūs spiežat "skaļāk", un nav jāzina, kā signāls tiek pārvērsts skaņā.

**Abstrakcija pret kapsulēšanu (bieži jaukti jēdzieni)**:

|                     | Abstrakcija                            | Kapsulēšana                                            |
| ------------------- | -------------------------------------- | ------------------------------------------------------ |
| Atbild uz jautājumu | **Ko** objekts dara? (dizaina līmenis) | **Kā** aizsargāt objekta datus? (realizācijas līmenis) |
| Mērķis              | Slēpt sarežģītību                      | Slēpt datus un nodrošināt to drošību                   |
| Piemērs             | Pults ar pogām                         | Slēgts korpuss, kam nevar piekļūt                      |
>[!Atceries]
Vienkāršoti: abstrakcija - _"lietotājs redz tikai vajadzīgo"_; 
kapsulēšana - _"lietotājs nevar piekļūt tam, kam nevajadzētu"_.

**Kā abstrakciju realizē C# valodā?** Ar:

1. **abstraktām klasēm** (`abstract class`) - daļēji gatavs šablons,
2. **interfeisiem** (`interface`) - par tiem vēlāk.

**Abstraktā klase** nedrīkst tikt izmantota, lai tieši izveidotu objektu (`new`). Tā kalpo kā pamats citām klasēm. Tajā var būt **abstraktas metodes** - metodes bez koda, kuras **obligāti jārealizē** atvasinātajām klasēm.

**Piemērs C#: ģeometriskās figūras**

```csharp
abstract class Shape
{
    public string Name;

    public Shape(string name)
    {
        Name = name;
    }

    // Abstrakta metode - nav koda, tikai "solījums"
    public abstract double CalculateArea();

    // Parasta metode ar kodu
    public void PrintInfo()
    {
        Console.WriteLine($"{Name}: laukums = {CalculateArea():F2}");
    }
}

class Circle : Shape
{
    public double Radius;

    public Circle(double radius) : base("Aplis")
    {
        Radius = radius;
    }

    public override double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}

class Rectangle : Shape
{
    public double Width;
    public double Height;

    public Rectangle(double width, double height) : base("Taisnstūris")
    {
        Width = width;
        Height = height;
    }

    public override double CalculateArea()
    {
        return Width * Height;
    }
}
```

```csharp
// Shape s = new Shape("Figūra");   // ❌ kļūda - abstraktu klasi nevar instancēt

Shape c = new Circle(5);
Shape r = new Rectangle(4, 6);

c.PrintInfo();   // Aplis: laukums = 78,54
r.PrintInfo();   // Taisnstūris: laukums = 24,00
```

Klase `Shape` apraksta **ko** katrai figūrai jāprot (aprēķināt laukumu), bet **kā** tas notiek - katra figūra izlemj pati. Lietotājs, kas izmanto `Shape`, šīs detaļas neredz.

> Šeit darbojas arī **polimorfisms** (`CalculateArea()` dažādiem objektiem dod dažādus rezultātus) un **mantošana** (`Circle : Shape`). Principi bieži strādā kopā.

---

## 7. Kopsavilkums

| Princips         | Galvenā doma                                | Dzīves piemērs                                           | C# atslēgvārdi                   |
| ---------------- | ------------------------------------------- | -------------------------------------------------------- | -------------------------------- |
| **Kapsulēšana**  | Slēpt datus, dot kontrolētu piekļuvi        | Kafijas automāts: pogas redzamas, spiediens nav pieejams | `private`, `public`, `get`/`set` |
| **Mantošana**    | Pārņemt un paplašināt citas klases iespējas | Transportlīdzeklis => Automašīna, Velosipēds              | `:`, `base`, `protected`         |
| **Polimorfisms** | Viena komanda - dažādas izpausmes           | "Skaņas" komanda: suns, kaķis, govs                      | `virtual`, `override`            |
| **Abstrakcija**  | Rādīt būtisko, slēpt sarežģīto              | Auto stūre un pedāļi                                     | `abstract`, `interface`          |

**Galvenās atziņas:**

1. **Klase** ir šablons, **objekts** ir konkrēts eksemplārs.
2. Objekta **lauki/īpašības** ir tā dati, **metodes** - tā uzvedība.
3. **Konstruktors** sagatavo objektu lietošanai brīdī, kad tas tiek izveidots.
4. Četri principi (kapsulēšana, mantošana, polimorfisms, abstrakcija) palīdz rakstīt kodu, ko ir **viegli saprast, mainīt un paplašināt**.

>[!Cheat sheet]
>**Klase** = recepte, **objekts** = kūka.
**Kapsulēšana** = kafijas automāta korpuss.
**Mantošana** = "IR" sakarība (Automašīna _ir_ Transportlīdzeklis).
**Polimorfisms** = viena komanda, daudz rezultātu.
**Abstrakcija** = pults, kas slēpj sarežģītību.
