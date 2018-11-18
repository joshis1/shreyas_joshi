---
layout: post
title:  "Builder_Pattern"
date:   2017-10-08 10:13:31 +1300
categories: Design_Patterns
---

This article is all about “Builder Pattern”. The “Builder Pattern” falls under
the category of creation software design pattern.

**What is a builder pattern?**

It is a pattern to construct a complex object , which is made of a simple
objects. Here, the recipe to make the complex object is only known to the
director. The builder knows the specifics to create the complex object , and it
is hidden from the client . The director calls the builder to build the
specifics.

**When is the ‘Builder Pattern’ required?**

It is required to create a number of objects, whose process of creation is
same. However, they differ in the representation. Basically, the construction
process/protocol is common, but the content is different . Here, the object is
build step by step with the aid of the director.

**How a ‘Builder Pattern’ is designed?**

1. Firstly, set a plan of the object that has the set of common behavioural
attributes. This is a sort of ‘Strategy/Behavioural Pattern’.
2. Create the concrete class from the strategy/behavioural interface class –
point number 1.
3. Make an abstract builder, which will set the attributes of the object.
4. Extend the abstract builder to create a concrete builder class. This should
set the attributes according to the desired concrete class.
5. Create a direct or class that will have the builder interface. The director
class should have the recipe to make the desired product using the builder
reference. The direct or class should also return the final product to the client .
6. It is a composition type where the ‘builder’ has the ‘object ’ – composition.
Also, the director has the builder reference – aggregation ( builder object –
specs is passed by the client ).

**Analogy:**

The director is like a waiter in the restaurant. The builders are the restaurant
staff . A client will speak t o director/waiter to order a product. Before ordering to the director, a client will get a specific(menu) from the builder. Also, a client will pass this specific to the waiter/director. Later, a direct or/waiter will prepare (build) the order and will pass to the client . In order to build the customer order, the waiter needs to interact with the builder. It will instruct the builder on what needs to be set.

**Problem/scenario:** In a Set -top box, we have a different types of tuners.
For example, terrestrial and satellite. All these tuners have the same
behaviours like – FEC, Polarisat ion, and modulation. However, the attributes
of these behaviours are different . Design a pattern to construct these objects.

**Analysis -** The terrestrial and satellite objects are having the similar kind of construction. However, they are represented differently. Here, we can use a
builder pattern to create these two objects.

Let’s see the UML diagram here.

<img src="/assets/img/Builder_Pattern_UML.png" alt="Builder_Pattern_UML">

1. The object interface is tuner here. The tuner has the following properties.

a. setTunerFEC()
b. setTunerPolarization()
c. setTunerModulationType()
This is nothing but a behaviour of the object – tuner.

2. Create a builder abstract class.
a. This should build the TunerFEC(), by calling the tuner behaviour methods –
setTunerFEC()
b. This should build the TunerPolarization(), by calling the tuner behaviour
methods – set TunerPolarization()
c. This should build the TunerModulationType(), by calling the tuner behaviour
methods – setTunerModulationType()

3. Create a concrete builder class – tunerTerrestrialBuilder()
4. Create a concrete builder class – tunerSatelliteBuilder()
5. Create a director/Engineer class that will build the final product. This will hold the reference to the builder. With the aid of a builder reference, it will call the specific build. For example, build TunerFEC, build
TunerPolarization(), and build setTunerModulationType().
6. Finally, the director will return the final product.
7. A client will create a builder type. For example, terrest rial t ype. Lat er, it will
pass t he t errest rial builder object t o t he direct or. T he direct or will call t he build
operat ions of t he t errest rial builder t o creat e a f inal product .
Interface or plan of the tuner object.
class Ituner
{
public:
virtual void setTunerFEC(float fec) = 0;
virtual void setTunerPolarization(std::string polar) = 0;
virtual void setTunerModulationType(std::string mod) = 0;
virtual ~Ituner();
};
Ituner::~Ituner()
{s
td::cout<<"Ituner destructor called"<<std::endl;
}
Concrete Tuner object to set the behaviour. A sort of strategy pattern.
class tuner: public Ituner
{
private:
float m_fec;
std::string m_polar;
std::string m_mod;
public:
tuner(): m_fec(0),m_polar("NONE"),m_mod("NONE")
{s
td::cout<<"Tuner Initialized"<<std::endl;
}
void setTunerFEC(float fec)
{m
_fec = fec;
}
float getTunerFEC(void)
{r
eturn m_fec;
}
void setTunerPolarization(std::string polar)
{m
_polar = polar;
}
std::string getTunerPolarization(void)
{r
eturn m_polar;
}
void setTunerModulationType(std::string mod)
{
m_mod = mod;
}
std::string getTunerModulationType(void)
{
return m_mod;
}
};
Here is the abstract builder class.
class ITunerBuilder
{
public:
virtual void buildTunerFEC() = 0;
virtual void buildTunerPolarization() = 0;
virtual void buildTunerModulationType() = 0;
virtual tuner getTuner() = 0;
virtual ~ITunerBuilder() = 0;
protected:
tuner m_tuner;
};
ITunerBuilder::~ITunerBuilder()
{s
td::cout<<"Virtual destructor of ItunerBuilder"<<std::endl;
}
Here is the concrete tuner builder – terrestrial type.
class tunerTerrestrialBuilder: public ITunerBuilder
{
public:
tunerTerrestrialBuilder()
{
}
~tunerTerrestrialBuilder()
{s
td::cout<<"Tuner terrestrial Builder deleted"<<std::endl;
}
void buildTunerFEC()
{m
_tuner.setTunerFEC(0.8);
}v
oid buildTunerPolarization()
{m
_tuner.setTunerPolarization("Vertical");
}v
oid buildTunerModulationType()
{m
_tuner.setTunerModulationType("QPSK");
}
tuner getTuner()
{r
eturn m_tuner;
}
};
Here is the concrete tuner builder – satellite type.
class tunerSatelliteBuilder: public ITunerBuilder
{
public:
tunerSatelliteBuilder()
{
}
~tunerSatelliteBuilder()
{s
td::cout<<"Tuner terrestrial Builder deleted"<<std::endl;
}
void buildTunerFEC()
{m
_tuner.setTunerFEC(0.75);
}v
oid buildTunerPolarization()
{m
_tuner.setTunerPolarization("Horizontal");
}v
oid buildTunerModulationType()
{m
_tuner.setTunerModulationType("QPSK2");
}
tuner getTuner()
{r
eturn m_tuner;
}
};
Let’s make a director/Engineer to take up the order of a client.
class tunerEngineer
{p
rivate:
ITunerBuilder *p_tunerBuilder;
/** forced to use the parameter constructor only **/
tunerEngineer();
public:
tunerEngineer(ITunerBuilder *tunerBuilder)
{
p_tunerBuilder = tunerBuilder;
}
tuner getTuner()
{r
eturn (p_tunerBuilder->getTuner());
}
void makeTuner()
{p
_tunerBuilder->buildTunerFEC();
p_tunerBuilder->buildTunerModulationType();
p_tunerBuilder->buildTunerPolarization();
}
};
Now, the main file for a client to test the builder pattern.
int main(void)
{t
uner terrestrialTuner;
/** this is a spec or a blue print that needs
* to be passed to the engineer/director**/
ITunerBuilder *pTerrBuilder = new tunerTerrestrialBuilder();
tunerEngineer *pTunerDirector = new tunerEngineer(pTerrBuilder);
pTunerDirector->makeTuner();
terrestrialTuner = pTunerDirector->getTuner();
std::cout<<"Terrestrial FEC TYPE is "<<terrestrialTuner.getTunerFEC()<<std::endl;
delete pTunerDirector;
delete pTerrBuilder;
tuner satelliteTuner;
ITunerBuilder *pSatBuilder = new tunerSatelliteBuilder();
pTunerDirector = new tunerEngineer(pSatBuilder);
pTunerDirector->makeTuner();
satelliteTuner = pTunerDirector->getTuner();
std::cout<<"Terrestrial FEC TYPE is "<<satelliteTuner.getTunerFEC()<<std::endl;
delete pTunerDirector;
delete pSatBuilder;
return 0;
}
Difference between Builder and Factory Pattern.
T he f act ory pat t ern creat es t he product in one st ep. However, t he builder
pat t ern creat es t he product in mult iple st eps. T he builder pat t ern uses
composit ion int ernally. It is a combinat ion of st rat egy/behavioural
pat t ern. Here, t he builder object ‘has a’ t uner object .
You can download t he ent ire code here.
