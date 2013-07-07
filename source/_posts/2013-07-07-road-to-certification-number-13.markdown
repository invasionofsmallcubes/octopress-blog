---
layout: post
title: "Road to Certification #13"
date: 2013-07-09 14:33
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
###Console
Console is abstract, there is no constructor. You get the console via `System.console()`. Useful methods are `String readLine("%s", "input: ")` and `char[] readPassword()`. 

##Serialization
You can serialize an object with all the instance variables (no static). The class must implement the interface `Serializable`. An attribute marked as **transient** will not be serialized.
<!-- more -->
You can serialize using an `Object(Output|Input)Stream` that accepts as input a `File(Output|Input)Stream`. Methods to put into the class are:

* `private void writeObject(ObjectOutputStream os) throws IOException`
* `private void readObject(ObjectInputStream is) throws IOException, ClassNotFound`

inside those methods you can do something like:

``` java SERIALIZATION
//write
os.defaultWriteObject();
os.writeInt(1);
//read
is.defaultReadObject();
int i = is.readInt();
// order between read and write is significant!!
```

If a class is serializable, in fase of deserialization the transient objects are initialized to the default value of the type they belong to, because the constructor is not called. If a superclass is not serializable, when the subclass is deserialized, the *default* constructor of the superclass is called. A really good example from stackoverflow:
``` java SERIALIZATION http://stackoverflow.com/questions/8141440/how-are-constructors-called-during-serialization-and-deserialization
public class ParentDeserializationTest {

public static void main(String[] args){
    try {
        System.out.println("Creating...");
        Child c = new Child(1);
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(baos);
        c.field = 10;
        System.out.println("Serializing...");
        oos.writeObject(c);
        oos.flush();
        baos.flush();
        oos.close();
        baos.close();
        ByteArrayInputStream bais = new ByteArrayInputStream(baos.toByteArray());
        ObjectInputStream ois = new ObjectInputStream(bais);
        System.out.println("Deserializing...");
        Child c1 = (Child)ois.readObject();
        System.out.println("c1.i="+c1.getI());
        System.out.println("c1.field="+c1.getField());
    } catch (IOException ex){
        ex.printStackTrace();
    } catch (ClassNotFoundException ex){
        ex.printStackTrace();
    }
}

public static class Parent {
    protected int field;
    protected Parent(){
        field = 5;
        System.out.println("Parent::Constructor");
    }
    public int getField() {
        return field;
    }
}

public static class Child extends Parent implements Serializable{
    protected int i;
    public Child(int i){
        this.i = i;
        System.out.println("Child::Constructor");
    }
    public int getI() {
        return i;
    }
}
```
If you serialize a Collection or an array, all objects contained in it must be `Serializable`.

