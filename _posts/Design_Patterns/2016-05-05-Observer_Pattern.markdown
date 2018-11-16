---
layout: post
title:  "2016-05-05"
date:   2016-01-11 14:13:31 +1300
categories: Design_Patterns
---

This article is all about ‘Observer Pattern’. This pattern is useful when the
dispatcher(Publisher) wants to notify the updates to all of the interested
clients. In short, we have a server that has all of the information, and it wants to post the information to all of the clients whenever the data changes.
The client needs to register with the server to get notification of any event
updates. Here the server is commonly known as the subject, and the client is
known as the observer. Also, we can say that subject is the publisher of the
information, and the observer is the subscriber of the information. This will be made clearer once we will describe the problem.

[note] - I have demonstrated this pattern using both C++ and Python.

**Problem** – In the broadcasting world, whenever the default settings of the
baud rate, video aspect ratio, and the default volume level needs to be
changed, the broadcast server will send the information to the client – a Set -
top box. So, the software component in the Set -top box, which gets to know
any updates is called the Update Manager, and the interested clients here are
– network component – for baud rate, display component for aspect ratio,
and the av component for the default volume level.

**Solution – Observer Pattern** -
The update Manager should notify all of the clients registered with it. These
clients can be network component , display component , and av component in
this example. Also, we should have a flexibility of adding or deleting these
clients at the run-time. So, here the publisher is – Update Manager and
subscribers are network component , av component , and display component.
Also, note that at any point of time any clients can be added or deleted. This
operation is at run-time.

Let’s make a UML representation of it .

<img src="/assets/img/ObserverPattern_UML.png" alt="ObserverPattern_UML">

So, let’s make an interface – subject class –

{% highlight ruby %}

class IPublisher
{
 public:
    virtual void registerObserver(ISubsrciber * observer) = 0;
    virtual void unregisterObserver(ISubsrciber * observer) = 0;
    virtual void setBaudRate(int newBaudRate) = 0;
    virtual void setAspectRatio(int newAspectRatio) = 0;
    virtual void setVolumeLevel(int newVolume) = 0;
    protected:
    virtual void notifyObserver() = 0;
};

{% endhighlight %}


Do remember that the interface is the class that has no fields, and all the
methods are pure virtual only. This interface has the following methods.
1. register observer
2. unregister observer
3. Event notifications like — baud rate change, aspect ratio Change, and
volume level change.
For the clarity, I have three methods here for all the updates – baud rate,
aspect ratio, and volume level.
I have a protected member – notifyObserver() – this will be internally be used
to notify the observers on any event updates like baud rate, aspect ratio, and
volume level. You might have noted that the server is dependent on the
observers. The publisher needs to maintain the list of subscribers here. Also,
the publisher needs to call the update routine of the subscriber.
Let’s have a look on the subscriber interface.

{% highlight ruby %}
class ISubsrciber
{
  public:
      virtual void update(int baudRate, int AspectRatio, int VolumeLevel) = 0;
};

{% endhighlight %}

The subscriber method – update() needs to be invoked by the server,
whenever the event is changed. Each concrete class called client will
implement the update() method. Here is the concrete subscriber class. Here,
we have created a client by registering it with the server. So, the constructor
of client will register with the server.

{% highlight ruby %}
class UpdateReceiver: public ISubsrciber
{
  private:
    int m_baudRate;
    int m_aspectRatio;
    int m_volumeLevel;
    int m_receiverNumber;
    static int updateReceiverTracker;
    /** Update Interface of the client ** /
public:
    /** Constructor -- and registers with the Server or Publisher or        UpdateManager ** /
    UpdateReceiver(IPublisher * updateManager)
    {
      m_receiverNumber = updateReceiverTracker++;
      updateManager->registerObserver(this);
    }
   void update(int baudRate, int AspectRatio, int VolumeLevel)
   {
     m_baudRate = baudRate;
     m_aspectRatio = AspectRatio;
     m_volumeLevel = VolumeLevel;
     qDebug()<<"The following client number : "<< m_receiverNumber<< " got the update ";
     qDebug()<<"The baudRate is "<<baudRate;
     qDebug()<<"The AspectRatio is"<<AspectRatio;
     qDebug()<<"The VolumeLevel is"<<VolumeLevel;
   }
};

{% endhighlight %}

Now, the Server/Publisher – the publisher needs to maintain the list of
observers. The observer gets added in the list when the register() method of
publisher is invoked. Here, we have registered the client to server on creation
only – check the constructor. The constructor calls the register() method of
the publisher. So, whenever the event is updated, it notifies to all the
observers. The interface to notify the observers is update(). Thus, a concrete
client needs to implement the update() method.

{% highlight ruby %}
class UpdateManager: public IPublisher
{
  private:
    QList<ISubsrciber * > subscribers;
    int m_baudRate;
    int m_aspectRatio;
    int m_volumeLevel;
  public:
    UpdateManager():m_baudRate(0),m_aspectRatio(0),m_volumeLevel(0)
    {
      qDebug()<<"Update Manager --- Server/Subject Initialized";
      subscribers.clear();
    }
    void registerObserver(ISubsrciber * observer)
    {
      subscribers.append(observer);
    }
    void unregisterObserver(ISubsrciber * observer)
    {
      int index = subscribers.indexOf(observer);
      subscribers.removeAt(index);
      qWarning()<<"Removed the subscriber Index = "<<index;  
    }
   void setBaudRate(int newBaudRate)
   {
      m_baudRate = newBaudRate;
      notifyObserver();
   }
   void setAspectRatio(int newAspectRatio)
   {
     m_aspectRatio = newAspectRatio;
     notifyObserver();
   }
   void setVolumeLevel(int newVolume)
   {
     m_volumeLevel = newVolume;
     notifyObserver();
   }
protected:
   void notifyObserver()
   {
     foreach( ISubsrciber * observer, subscribers )
     {
       observer->update(m_baudRate,m_aspectRatio,m_volumeLevel);
     }
   }
};

{% endhighlight %}

Here is the main(). The two clients are created. They both will get the
notification, whenever the event is updated. However, at any time we can
deregister any client . Also, we can add/register more clients.

{% highlight ruby %}

int main(int argc, char * argv[])
{
  QCoreApplication a(argc, argv);
  IPublisher * AV_UpdateMgr = new UpdateManager();
  ISubsrciber * AV_UpdateReceiver = new UpdateReceiver(AV_UpdateMgr);
  ISubsrciber * NW_UpdateReceiver = new UpdateReceiver(AV_UpdateMgr);
  /** Server Updating the values ** /
  AV_UpdateMgr->setBaudRate(1000);
  AV_UpdateMgr->setAspectRatio(43);
  AV_UpdateMgr->setVolumeLevel(100);
  AV_UpdateMgr->unregisterObserver(AV_UpdateReceiver);
  AV_UpdateMgr->setVolumeLevel(100);
  delete AV_UpdateReceiver;
  delete AV_UpdateMgr;
  delete NW_UpdateReceiver;
  return a.exec();
}

{% endhighlight %}

Here is the result.

<img src="/assets/img/ObserverPattern_Output.png" alt="ObserverPattern_Output">

The entire code can be downloaded below. Here the code is written in Python.

[Source_code_ObserverPattern](https://drive.google.com/open?id=1SPHpEjtD0MnGXIcL5ZEL7lPqAvEdQsoc)

**When to use Observer Pattern?**
Whenever an update is to be published to multiple clients. It is like one to
many relationship.

**Advantage of Observer Pattern -**
With the help of interface, the subject/publisher doesn’t need to know
anything about the observers.

**Disadvantage of Observer Pattern -**
The subject /publisher may send multiple updates even when the component is
not interested. For example, baud rate change is not an interested event for
the display module. However, the client will get it . Nevertheless, a client can
have an internal logic, where they can check for the interested event field
update.

Examples of Observer Pattern – Signal/Slots in Qt .
