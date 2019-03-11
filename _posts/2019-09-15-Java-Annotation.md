---
layout: post
title: Java Annotation
category: java
tags: [java]
---

Annotations is a form of **metadata** which provide data about a program that is not part of the program itself. Annotations have **no direct effect on the operation of the code they annotate**.

Annotations have a number of uses, among them:

* **Information for the compiler** — Annotations can be used by the compiler to detect errors or suppress warnings.
* **Compile-time and deployment-time** processing — Software tools can process annotation information to generate code, XML files, and so forth.
* **Runtime processing** — Some annotations are available to be examined at runtime.

## Predefined Annotations

A set of annotation types are already predefined in the Java SE API in `java.lang`. They are:

1. `@Override`
2. `@Deprecated`
3. `@SuppressWarnings`

### @Override

`@Override` informs the compiler that the marked method is meant to override a method in a superclass. If a method with `@Override` fails to override a method in one of its superclasses, a wrong method name for example, the compiler generates an error. It can only be used for methods.

{% highlight java %}
public class Fruit {
    public void eat(){
        System.out.println("Eat fruit");
    }
}

class Orange extends Fruit {
    @Override
    public void eat(){
        System.out.println("eat orange");
    }
}

class Apple extends Fruit {
    // wrong method name here
    @Override
    public void aet(){
        System.out.println("eat apple");
    }
}
{% endhighlight %}

When compile class Apple, it will generate an override error because of wrong method name.

### @Deprecated

It indicates that the marked element is deprecated and should no longer be used. The compiler generates a **warning** whenever a program uses a method, class, or field with the @Deprecated annotation.

It also has a certain "inheritance": **If we use in the code an overrided/inherited types or methods from deprecated ones, the compiler still generates a warning**.

{% highlight java %}
public class Fruit {
    @Deprecated
    public void eat(){
        System.out.println("Eat fruit");
    }
}

class Orange extends Fruit {
    @Override
    public void eat(){
        System.out.println("eat orange");
    }
}
{% endhighlight %}

So we would get a warning when use eat() in class Orange.

### @SuppressWarnings

It tells compiler to suppress specific warnings that it would otherwise generate. In the following example, a deprecated method is used but now `@SuppressWarnings` causes the warning to be suppressed.

{% highlight java %}
public class Fruit {
    @Deprecated
    public void eat(){
        System.out.println("Eat fruit");
    }
}

class Orange extends Fruit {
    @SuppressWarnings("deprecation")
    @Override
    public void eat(){
        System.out.println("eat orange");
    }
}
{% endhighlight %}

This annotation has a String[] parameter. 

* @SuppressWarnings(value={ "rawtypes", "unchecked" }) - When two warnings to suppress
* @SuppressWarnings({"unchecked", "deprecation"}) - "value=" could be ignored
* @SuppressWarnings("deprecation") - We could write like this if only one parameter

The following is some common warnings:

> It depends on jdk and ide, more details [here](http://stackoverflow.com/questions/1205995/what-is-the-list-of-valid-suppresswarnings-warning-names-in-java)

1. deprecation：to suppress warnings relative to deprecation
2. unchecked：to suppress warnings relative to unchecked operations
3. fallthrough：to suppress warnings relative to missing breaks in switch statements
4. cast: to suppress warnings relative to cast operations
5. serial：to suppress warnings relative to missing serialVersionUID field for a serializable class
6. finally：to suppress warnings relative to finally block that don't retur
7. unused: to suppress warnings relative to unused code and dead code
8. all：to suppress all warnings


## Meta-Annotations

**Meta-Annotations are annotations which will be applied to other annotations**. It's just like meta-data. When you define your own annotation, you must use them. There are several meta-annotation types defined in `java.lang.annotation`.

1. `@Target`
2. `@Retention`
3. `@Documented`
4. `@Inherited`

### @Target

`@Target` marks another annotation to ＊＊restrict what kind of Java elements the annotation can be applied to＊＊. A target annotation specifies one of the following element types as its value:

*  `ElementType.ANNOTATION_TYPE` can be applied to an annotation type.
*  `ElementType.CONSTRUCTOR` can be applied to a constructor.
*  `ElementType.FIELD` can be applied to a field or property.
*  `ElementType.LOCAL_VARIABLE` can be applied to a local variable.
*  `ElementType.METHOD` can be applied to a method-level annotation.
*  `ElementType.PACKAGE` can be applied to a package declaration.
*  `ElementType.PARAMETER` can be applied to the parameters of a method.
*  `ElementType.TYPE` can be applied to any element of a class.

{% highlight java %}
@Target(ElementType.TYPE)
public @interface Table {
    //......
}

@Target(ElementType.FIELD)
public @interface NoDBColumn {
	//......
}
{% endhighlight %}

So annotation @Table can be used for class/interface/enum. @NoDBColumn can be used for field or property of a class.

### @Retention

`@Retention` specifies how the marked annotation is stored or could be considered as its lifecycle:

* `RetentionPolicy.SOURCE` – The annotation is retained only in the source level and is ignored by the compiler.
* `RetentionPolicy.CLASS` – The annotation is retained by the compiler at compile time, but is ignored by the JVM.
* `RetentionPolicy.RUNTIME` – The annotation is retained by the JVM so it can be used by the runtime environment.

{% highlight java %}
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Column {
    public String name() default "fieldName";
    public String setFuncName() default "setField";
    public String getFuncName() default "getField"; 
    public boolean defaultDBValue() default false;
}
{% endhighlight %}

So here, Column annotation is retained by the JVM at runtime, we could get its properties by java reflection to do some more operations!

Only if when we declare retention as `RetentionPolicy.RUNTIME`, we could get the parameters of annotation by java reflection api to do some other operations.

### @Documented

`@Documented` indicates that **whenever the specified annotation is used those elements should be documented using the Javadoc tool**. 

### @Inherited

`Inherited` indicates that the annotation type can be inherited from the super class. (This is not true by default.). **If an annotation with `@Inherited` is applied to a class, so all its subclasses will also have this annotation**. For exemple: `@Deprecated`


## Customize Annotations

The format to define an annotation:

{% highlight java %}
@Meta-Annotation A
@Meta-Annotation B
public @interface annotationName {
    returnType functionA() default defaultValueA;
    returnType functionB() default defaultValueB;
}
{% endhighlight %}

When we use `@interface`, it implements automatically `java.lang.annotation.Annotation` interface. Every method in it is actually a configuration parameter. Name of the method is the name of the parameter, returnType is the type of argument(returnType can only be a basic type, Class, String, enum). You can declare the default value of the parameter.

It supports the following types:

1. All basic types（int,float,boolean,byte,double,char,long,short)
2. String
3. Class
4. enum
5. Annotation
6. All above in array

>When we define an annotation, it can not inherit other annotations or interfaces.
>Only public or default is allowed for functions.
>If only one parameter, better to set the name as "value". So we could ignore "value=" when use this annotation.

### Example

Define now `@MethodInfo` to indicate information about a method

{% highlight java %}
@Target(ElementType.METHOD)
@Inherited
@Retention(RetentionPolicy.RUNTIME)
public @interface MethodInfo{

    String author() default "Dong";
    String date();
    int revision() default 1;
    String comments();
    
}
{% endhighlight %}

So by its meta annotations, we could know that:

* `@Target(ElementType.METHOD)` -> It could only mark methods
* `@Inherited` -> All the override functions in the subclasses will be added this annotations automatically
* `@Retention(RetentionPolicy.RUNTIME)` -> So we could get the configuration parameters set in this annotations by java reflection api at runtime

Now we use this annotation on a method

{% highlight java %} 
public class AnnotationExample {
 
    @MethodInfo(author = "Dong", comments = "An example", date = "26 12 2015", revision = 3)
    public String todo() {
        return "I use annotations!";
    }
    
}
{% endhighlight %}

Then we will use the Java reflection to parse `@MethodInfo` in order to know information about the method marked by this annotation.

{% highlight java %} 
public class AnnotationParsing {
 
    public static void main(String[] args) {
        try {
            for (Method method : AnnotationParsing.class
                    .getClassLoader()
                    .loadClass(("com.dong.annotations.AnnotationExample"))
                    .getMethods()) {
                // checks if MethodInfo annotation is present for the method
                if (method
                        .isAnnotationPresent(com.dong.annotations.MethodInfo.class)) {
                    try {
                        // iterates all the annotations available in the method
                        for (Annotation anno : method.getDeclaredAnnotations()) {
                            System.out.println("Annotation in Method '"
                                    + method + "' : " + anno);
                        }
                        MethodInfo methodAnno = method
                                .getAnnotation(MethodInfo.class);
                        if (methodAnno.revision() == 1) {
                            System.out.println("Method with revision no 1 = "
                                    + method);
                        }
 
                    } catch (Throwable ex) {
                        ex.printStackTrace();
                    }
                }
            }
        } catch (SecurityException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
 
}

{% endhighlight %}

Output：

{% highlight java %} 
Annotation in Method 'public java.lang.String com.dong.annotations.AnnotationExample.todo()' : @com.dong.annotations.MethodInfo(author=Pankaj, revision=1, comments=An example, date=Nov 17 2012)
Method with revision no 1 = public java.lang.String com.dong.annotations.AnnotationExample.todo()
{% endhighlight %}

## Ref
- [Oracle Java Doc](https://docs.oracle.com/javase/tutorial/java/annotations/)
- [Wiki - Java Annotation](https://fr.wikipedia.org/wiki/Annotation_(Java))
