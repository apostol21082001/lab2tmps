# Tehnici și Mecanisme de Proiectare Software

Labortator nr.2

Apostol Mihail,ti_204


Au fost alese 5 șabloane:
1. Singleton
Acesta este un model de design generațional care asigură că o clasă are o singură instanță și oferă un punct de acces global la aceasta.

structura șablonului singleton
![Структура шаблона одиночка](https://refactoring.guru/images/patterns/diagrams/singleton/structure-ru-2x.png )

Pentru a implementa acest model, a fost creată o clasă [Map](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Map/Map.cs)
```
public class Map
{
    private static Map MapObject;
    ***
    public static Size Size;
    private Map(Point p,int height, int width)
    {
        Size = new Size(width, height);
        PointStart = p;
        GameField = new Rectangle(PointStart, Size);
        Graphics.FillRectangle(new SolidBrush(Color.OldLace), GameField);
    }
    ***
    public static Map GetInstance(Point p, int height, int width, Graphics gs)
    {
        if (MapObject == null)
        {
            Graphics = gs;
            MapObject = new Map(p, height, width);
            return MapObject;
        }
        else
            return MapObject;
    }
    ***
}
```
Acest șablon a fost folosit deoarece aveam nevoie de o singură inițializare a hărții în aplicație
2. Factory Method

Este un model de design generativ care definește o interfață comună pentru crearea de obiecte într-o superclasă, permițând subclaselor să schimbe tipul de obiecte pe care le creează.

Modelul metodei Factory propune ca obiectele să nu fie create direct folosind operatorul nou, ci apelând o metodă specială din fabrică. Obiectele vor fi în continuare create cu noi, dar metoda din fabrică o va face.

![Image of Factory Method](https://refactoring.guru/images/patterns/cards/factory-method-mini-2x.png)

Utilizarea clasei Abstracte [clasei abstracte](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Factory/AbstractObject.cs) in
```
public abstract class AbstractObject : IObjectBuilder
{
  ***
}
```
Pentru ca acest sistem să funcționeze, toate obiectele returnate trebuie să aibă o interfață comună.
Pentru anuntarea [clasa, ce raspunde de cercuri](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Factory/Circle/CircleBuilder.cs) in program:
```
public class CircleBuilder : AbstractObject, IObjectBuilder
{
  ***
}
```
Pentru anuntarea [clasa, ce raspunde de patrate](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Factory/Rectangle/RectangleBuilder.cs)

```
public class RectangleBuilder: AbstractObject, IObjectBuilder
{
  ***
}
```

3. Abstract Factory

Acesta este un model de design generativ care vă permite să creați familii de obiecte înrudite fără a fi legat de clasele specifice de obiecte pe care le creați.
![Image of Abstract Factory](https://refactoring.guru/images/patterns/cards/abstract-factory-mini-2x.png)

Iterface a fost anunțat in urmatorul [file](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Factory/IUnitFactory.cs)
```
public interface IUnitFactory
{
    string Name { get; set; }
    IObjectBuilder ObjectBuilder { get; }       

}
```

Clasele descendente sunt create în următoarele fișiere  [file1](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Factory/CircleFactory.cs)  [file2](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Factory/RectangleFactory.cs)

```
public class RectangleFactory : IUnitFactory
{
  ***
}
public class CircleFactory : IUnitFactory
{
  ***
}
```


4. Builder

Este un model de design generativ care vă permite să creați obiecte complexe pas cu pas. Constructorul face posibilă utilizarea aceluiași cod de construcție pentru a obține reprezentări diferite ale obiectelor.
![Image of Builder](https://refactoring.guru/images/patterns/diagrams/builder/solution1-2x.png)

Constructorul vă permite să creați obiecte complexe pas cu pas. Rezultatul intermediar rămâne întotdeauna protejat.
Prezentarea [Object builder interface](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Factory/IObjectBuilder.cs)

```
public interface IObjectBuilder
{       
Graphics formGraphics { get; set; }
IObjectBuilder BuildObject();
UserColor ObjectColor { get; set; }
void ChangeColor();

}
```
Puteți verifica implementarea acestei interfețe în Factory Method.
Clasele CircleBuilder și RectangleBuilder îl implementează.

5. Prototype

Acesta este un model de design generativ care vă permite să copiați obiecte fără a intra în detaliile implementării lor. Următorul este un exemplu de structură de șablon prototip
![Image of Prototype](https://refactoring.guru/images/patterns/diagrams/prototype/structure-2x.png)

Prototipul a fost folosit pentru [cercuri](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Factory/Circle/CircleBuilder.cs)
, de asemenea si pentru[patrate](https://github.com/apostol21082001/lab2tmps/blob/main/patternLab/Factory/Rectangle/RectangleBuilder.cs)

Metodele de mai jos returnează o nouă instanță de obiect.

```
public static CircleBuilder CopyCircle(CircleBuilder tempCircle)
{
    CircleBuilder temp = new CircleBuilder(tempCircle.formGraphics, tempCircle.ThisObject, tempCircle.ObjectColor,
        tempCircle.timer);

    return temp;
}

public static RectangleBuilder CopyRectangle(RectangleBuilder tempRectangle)
{
    RectangleBuilder temp = new RectangleBuilder(tempCircle.formGraphics, tempCircle.ThisObject, tempCircle.ObjectColor,
        tempCircle.timer);

    return temp;
}
```

Am folosit acest model pentru a copia cercuri și pătrate.


Rezultatul:
![Image of program](https://github.com/apostol21082001/lab2tmps/blob/main/rezultat.jpg)

Concluzie:
 Pe parcursul acestei lucrări de laborator, am studiat și implementat creational design pattern, ele simplifică și structurează codul pentru noi.
