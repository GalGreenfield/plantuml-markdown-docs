# Drawing UML with PlantUML

## PlantUML Language Reference Guide

### (Version 1.2019.9)

**PlantUML** is a component that allows to quickly write :

- Sequence diagram
- Usecase diagram
- Class diagram
- Activity diagram
- Component diagram
- State diagram
- Object diagram
- Deployment diagram
- Timing diagram

The following non-UML diagrams are also supported:

- Wireframe graphical interface
- Archimate diagram
- Specification and Description Language (SDL)
- Ditaa diagram
- Gantt diagram
- MindMap diagram
- Work Breakdown Structure diagram
- Mathematic with AsciiMath or JLaTeXMath notation

Diagrams are defined using a simple and intuitive language.


#### 1 SEQUENCE DIAGRAM

## 1 Sequence Diagram

### 1.1 Basic examples

The sequence->is used to draw a message between two participants. Participants do not have to be explicitly
declared.

To have a dotted arrow, you use-->

It is also possible to use<-and<--. That does not change the drawing, but may improve readability. Note that
this is only true for sequence diagrams, rules are different for the other diagrams.

@startuml
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response

Alice -> Bob: Another authentication Request
Alice <-- Bob: Another authentication Response
@enduml

### 1.2 Declaring participant

If the keywordparticipantis used to declare a participant, more control on that participant is possible.

The order of declaration will be the (default) **order of display**.

Using these other keywords to declare participants will **change the shape** of the participant representation:

- actor
- boundary
- control
- entity
- database
- collections

@startuml
actor Foo
boundary Foo
control Foo
entity Foo
database Foo
collections Foo
Foo1 -> Foo2 : To boundary
Foo1 -> Foo3 : To control
Foo1 -> Foo4 : To entity
Foo1 -> Foo5 : To database
Foo1 -> Foo6 : To collections


_1.2 Declaring participant 1 SEQUENCE DIAGRAM_

@enduml

Rename a participant using theaskeyword.

You can also change the background color of actor or participant.

@startuml
actor Bob #red
' The only difference between actor
'and participant is the drawing
participant Alice
participant "I have a really\nlong name" as L #99FF
/' You can also declare:
participant L as "I have a really\nlong name" #99FF
'/

Alice->Bob: Authentication Request
Bob->Alice: Authentication Response
Bob->L: Log transaction
@enduml

You can use theorderkeyword to customize the display order of participants.

@startuml
participant Last order 30
participant Middle order 20
participant First order 10
@enduml


_1.3 Use non-letters in participants 1 SEQUENCE DIAGRAM_

### 1.3 Use non-letters in participants

You can use quotes to define participants. And you can use theaskeyword to give an alias to those participants.

@startuml
Alice -> "Bob()" : Hello
"Bob()" -> "This is very\nlong" as Long
' You can also declare:
' "Bob()" -> Long as "This is very\nlong"
Long --> "Bob()" : ok
@enduml

### 1.4 Message to Self

A participant can send a message to itself.

It is also possible to have multi-line using\n.

@startuml
Alice->Alice: This is a signal to self.\nIt also demonstrates\nmultiline \ntext
@enduml

### 1.5 Change arrow style

You can change arrow style by several ways:

- add a finalxto denote a lost message
- use\or/instead of<or>to have only the bottom or top part of the arrow
- repeat the arrow head (for example,>>or//) head to have a thin drawing
- use--instead of-to have a dotted arrow


_1.6 Change arrow color 1 SEQUENCE DIAGRAM_

- add a final "o" at arrow head
- use bidirectional arrow<->

@startuml
Bob ->x Alice
Bob -> Alice
Bob ->> Alice
Bob -\ Alice
Bob \\- Alice
Bob //-- Alice

Bob ->o Alice
Bob o\\-- Alice

Bob <-> Alice
Bob <->o Alice
@enduml

### 1.6 Change arrow color

You can change the color of individual arrows using the following notation:

@startuml
Bob -[#red]> Alice : hello
Alice -[#0000FF]->Bob : ok
@enduml

### 1.7 Message sequence numbering

The keywordautonumberis used to automatically add number to messages.

@startuml
autonumber
Bob -> Alice : Authentication Request
Bob <- Alice : Authentication Response
@enduml


_1.7 Message sequence numbering 1 SEQUENCE DIAGRAM_

You can specify a startnumber withautonumber _start_ , and also an increment withautonumber _start
increment_.

@startuml
autonumber
Bob -> Alice : Authentication Request
Bob <- Alice : Authentication Response

autonumber 15
Bob -> Alice : Another authentication Request
Bob <- Alice : Another authentication Response

autonumber 40 10
Bob -> Alice : Yet another authentication Request
Bob <- Alice : Yet another authentication Response

@enduml

You can specify a format for your number by using between double-quote.

The formatting is done with the Java classDecimalFormat( 0 means digit,#means digit and zero if absent).

You can use some html tag in the format.

@startuml
autonumber "<b>[000]"
Bob -> Alice : Authentication Request
Bob <- Alice : Authentication Response

autonumber 15 "<b>(<u>##</u>)"
Bob -> Alice : Another authentication Request
Bob <- Alice : Another authentication Response

autonumber 40 10 "<font color=red><b>Message 0 "
Bob -> Alice : Yet another authentication Request
Bob <- Alice : Yet another authentication Response

@enduml


_1.8 Page Title, Header and Footer 1 SEQUENCE DIAGRAM_

You can also useautonumber stopandautonumber resume _increment format_ to respectively pause and
resume automatic numbering.

@startuml
autonumber 10 10 "<b>[000]"
Bob -> Alice : Authentication Request
Bob <- Alice : Authentication Response

autonumber stop
Bob -> Alice : dummy

autonumber resume "<font color=red><b>Message 0 "
Bob -> Alice : Yet another authentication Request
Bob <- Alice : Yet another authentication Response

autonumber stop
Bob -> Alice : dummy

autonumber resume 1 "<font color=blue><b>Message 0 "
Bob -> Alice : Yet another authentication Request
Bob <- Alice : Yet another authentication Response
@enduml

### 1.8 Page Title, Header and Footer

Thetitlekeyword is used to add a title to the page.


_1.9 Splitting diagrams 1 SEQUENCE DIAGRAM_

Pages can display headers and footers usingheaderandfooter.

@startuml

header Page Header
footer Page %page% of %lastpage%

title Example Title

Alice -> Bob : message 1
Alice -> Bob : message 2

@enduml

### 1.9 Splitting diagrams

Thenewpagekeyword is used to split a diagram into several images.

You can put a title for the new page just after thenewpagekeyword. This title overrides the previously specified
title if any.

This is very handy with _Word_ to print long diagram on several pages.

(Note: this really does work. Only the first page is shown below, but it is a display artifact.)

@startuml

Alice -> Bob : message 1
Alice -> Bob : message 2

newpage

Alice -> Bob : message 3
Alice -> Bob : message 4

newpage A title for the\nlast page

Alice -> Bob : message 5
Alice -> Bob : message 6
@enduml


_1.10 Grouping message 1 SEQUENCE DIAGRAM_

### 1.10 Grouping message

It is possible to group messages together using the following keywords:

- alt/else
- opt
- loop
- par
- break
- critical
- group, followed by a text to be displayed

It is possible a add a text that will be displayed into the header (except forgroup).

Theendkeyword is used to close the group.

Note that it is possible to nest groups.

@startuml
Alice -> Bob: Authentication Request

alt successful case

Bob -> Alice: Authentication Accepted

else some kind of failure

Bob -> Alice: Authentication Failure
group My own label
Alice -> Log : Log attack start
loop 1000 times
Alice -> Bob: DNS Attack
end
Alice -> Log : Log attack end
end

else Another type of failure

```
Bob -> Alice: Please repeat
```
end
@enduml


_1.11 Notes on messages 1 SEQUENCE DIAGRAM_

### 1.11 Notes on messages

It is possible to put notes on message using thenote leftornote rightkeywords _just after the message_.

You can have a multi-line note using theend notekeywords.

@startuml
Alice->Bob : hello
note left: this is a first note

Bob->Alice : ok
note right: this is another note

Bob->Bob : I am thinking
note left
a note
can also be defined
on several lines
end note
@enduml


_1.12 Some other notes 1 SEQUENCE DIAGRAM_

### 1.12 Some other notes

It is also possible to place notes relative to participant withnote left of,note right ofornote over
keywords.

It is possible to highlight a note by changing its background color.

You can also have a multi-line note using theend notekeywords.

@startuml
participant Alice
participant Bob
note left of Alice #aqua
This is displayed
left of Alice.
end note

note right of Alice: This is displayed right of Alice.

note over Alice: This is displayed over Alice.

note over Alice, Bob #FFAAAA: This is displayed\n over Bob and Alice.

note over Bob, Alice
This is yet another
example of
a long note.
end note
@enduml

### 1.13 Changing notes shape

You can usehnoteandrnotekeywords to change note shapes.

@startuml
caller -> server : conReq
hnote over caller : idle
caller <- server : conConf
rnote over server
"r" as rectangle
"h" as hexagon


_1.14 Creole and HTML 1 SEQUENCE DIAGRAM_

endrnote
@enduml

### 1.14 Creole and HTML

It is also possible to use creole formatting:

@startuml
participant Alice
participant "The **Famous** Bob" as Bob

Alice -> Bob : hello --there--
... Some ~~long delay~~ ...
Bob -> Alice : ok
note left
This is **bold**
This is //italics//
This is ""monospaced""
This is --stroked--
This is __underlined__
This is ~~waved~~
end note

Alice -> Bob : A //well formatted// message
note right of Alice
This is <back:cadetblue><size:18>displayed</size></back>
__left of__ Alice.
end note
note left of Bob
<u:red>This</u> is <color #118888>displayed</color>
**<color purple>left of</color> <s:red>Alice</strike> Bob**.
end note
note over Alice, Bob
<w:#FF33FF>This is hosted</w> by <img sourceforge.jpg>
end note
@enduml


_1.15 Divider 1 SEQUENCE DIAGRAM_

### 1.15 Divider

If you want, you can split a diagram using==separator to divide your diagram into logical steps.

@startuml

== Initialization ==

Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response

== Repetition ==

Alice -> Bob: Another authentication Request
Alice <-- Bob: another authentication Response

@enduml


_1.16 Reference 1 SEQUENCE DIAGRAM_

### 1.16 Reference

You can use reference in a diagram, using the keywordref over.

@startuml
participant Alice
actor Bob

ref over Alice, Bob : init

Alice -> Bob : hello

ref over Bob
This can be on
several lines
end ref
@enduml

### 1.17 Delay

You can use...to indicate a delay in the diagram. And it is also possible to put a message with this delay.

@startuml


_1.18 Space 1 SEQUENCE DIAGRAM_

Alice -> Bob: Authentication Request
...
Bob --> Alice: Authentication Response
...5 minutes later...
Bob --> Alice: Bye!

@enduml

### 1.18 Space

You can use|||to indicate some spacing in the diagram.

It is also possible to specify a number of pixel to be used.

@startuml

Alice -> Bob: message 1
Bob --> Alice: ok
|||
Alice -> Bob: message 2
Bob --> Alice: ok
||45||
Alice -> Bob: message 3
Bob --> Alice: ok

@enduml


_1.19 Lifeline Activation and Destruction 1 SEQUENCE DIAGRAM_

### 1.19 Lifeline Activation and Destruction

Theactivateanddeactivateare used to denote participant activation.

Once a participant is activated, its lifeline appears.

Theactivateanddeactivateapply on the previous message.

Thedestroydenote the end of the lifeline of a participant.

@startuml
participant User

User -> A: DoWork
activate A

A -> B: << createRequest >>
activate B

B -> C: DoWork
activate C
C --> B: WorkDone
destroy C

B --> A: RequestCreated
deactivate B

A -> User: Done
deactivate A

@enduml

Nested lifeline can be used, and it is possible to add a color on the lifeline.

@startuml
participant User

User -> A: DoWork
activate A #FFBBBB

A -> A: Internal call
activate A #DarkSalmon

A -> B: << createRequest >>
activate B

B --> A: RequestCreated


_1.20 Return 1 SEQUENCE DIAGRAM_

deactivate B
deactivate A
A -> User: Done
deactivate A

@enduml

Autoactivation is possible and works with the return keywords:

@startuml
autoactivate on
alice -> bob : hello
bob -> bob : self call
bill -> bob #005500 : hello from thread 2
bob -> george ** : create
return done in thread 2
return rc
bob -> george !! : delete
return success
@enduml

### 1.20 Return

Commandreturngenerates a return message with optional text label.

The return point is that which caused the most recent life-line activation.


_1.21 Participant creation 1 SEQUENCE DIAGRAM_

The syntax isreturn labelwherelabelif provided is any string acceptable for conventional messages.

@startuml
Bob -> Alice : hello
activate Alice
Alice -> Alice : some action
return bye
@enduml

### 1.21 Participant creation

You can use thecreatekeyword just before the first reception of a message to emphasize the fact that this message
is actually _creating_ this new object.

@startuml
Bob -> Alice : hello

create Other
Alice -> Other : new

create control String
Alice -> String
note right : You can also put notes!

Alice --> Bob : ok

@enduml

### 1.22 Shortcut syntax for activation, deactivation, creation

Immediately after specifying the target participant, the following syntax can be used:

- ++Activate the target (optionally a #color may follow this)


_1.23 Incoming and outgoing messages 1 SEQUENCE DIAGRAM_

- --Deactivate the source
- **Create an instance of the target
- !!Destroy an instance of the target

@startuml
alice -> bob ++ : hello
bob -> bob ++ : self call
bob -> bib ++ #005500 : hello
bob -> george ** : create
return done
return rc
bob -> george !! : delete
return success
@enduml

### 1.23 Incoming and outgoing messages

You can use incoming or outgoing arrows if you want to focus on a part of the diagram.

Use square brackets to denote the left "[" or the right "]" side of the diagram.

@startuml
[-> A: DoWork

activate A

A -> A: Internal call
activate A

A ->] : << createRequest >>

A<--] : RequestCreated
deactivate A
[<- A: Done
deactivate A
@enduml


_1.24 Anchors and Duration 1 SEQUENCE DIAGRAM_

You can also have the following syntax:

@startuml
[-> Bob
[o-> Bob
[o->o Bob
[x-> Bob

[<- Bob
[x<- Bob

Bob ->]
Bob ->o]
Bob o->o]
Bob ->x]

Bob <-]
Bob x<-]
@enduml

### 1.24 Anchors and Duration

Withteozusage it is possible to add anchors to the diagram and use the anchors to specify duration time.

@startuml
!pragma teoz true

{start} Alice -> Bob : start doing things during duration
Bob -> Max : something
Max -> Bob : something else
{end} Bob -> Alice : finish


_1.25 Stereotypes and Spots 1 SEQUENCE DIAGRAM_

{start} <-> {end} : some time

@enduml

### 1.25 Stereotypes and Spots

It is possible to add stereotypes to participants using<<and>>.

In the stereotype, you can add a spotted character in a colored circle using the syntax(X,color).

@startuml

participant "Famous Bob" as Bob << Generated >>
participant Alice << (C,#ADD1B2) Testable >>

Bob->Alice: First message

@enduml

By default, the _guillemet_ character is used to display the stereotype. You can change this behavious using the
skinparamguillemet:

@startuml

skinparam guillemet false
participant "Famous Bob" as Bob << Generated >>
participant Alice << (C,#ADD1B2) Testable >>

Bob->Alice: First message

@enduml


_1.26 More information on titles 1 SEQUENCE DIAGRAM_

@startuml

participant Bob << (C,#ADD1B2) >>
participant Alice << (C,#ADD1B2) >>

Bob->Alice: First message

@enduml

### 1.26 More information on titles

You can use creole formatting in the title.

@startuml

title __Simple__ **communication** example

Alice -> Bob: Authentication Request
Bob -> Alice: Authentication Response

@enduml

You can add newline using\nin the title description.

@startuml

title __Simple__ communication example\non several lines

Alice -> Bob: Authentication Request
Bob -> Alice: Authentication Response

@enduml


_1.27 Participants encompass 1 SEQUENCE DIAGRAM_

You can also define title on several lines usingtitleandend titlekeywords.

@startuml

title
<u>Simple</u> communication example
on <i>several</i> lines and using <font color=red>html</font>
This is hosted by <img:sourceforge.jpg>
end title

Alice -> Bob: Authentication Request
Bob -> Alice: Authentication Response

@enduml

### 1.27 Participants encompass

It is possible to draw a box around some participants, usingboxandend boxcommands.

You can add an optional title or a optional background color, after theboxkeyword.

@startuml

box "Internal Service" #LightBlue
participant Bob
participant Alice
end box
participant Other

Bob -> Alice : hello
Alice -> Other : hello

@enduml


_1.28 Removing Foot Boxes 1 SEQUENCE DIAGRAM_

### 1.28 Removing Foot Boxes

You can use thehide footboxkeywords to remove the foot boxes of the diagram.

@startuml

hide footbox
title Foot Box removed

Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response

@enduml

### 1.29 Skinparam

You can use theskinparamcommand to change colors and fonts for the drawing.

You can use this command:

- In the diagram definition, like any other commands,
- In an included file,
- In a configuration file, provided in the command line or the ANT task.

You can also change other rendering parameter, as seen in the following examples:

@startuml
skinparam sequenceArrowThickness 2
skinparam roundcorner 20
skinparam maxmessagesize 60
skinparam sequenceParticipant underline

actor User
participant "First Class" as A
participant "Second Class" as B
participant "Last Class" as C

User -> A: DoWork
activate A


_1.29 Skinparam 1 SEQUENCE DIAGRAM_

A -> B: Create Request
activate B

B -> C: DoWork
activate C
C --> B: WorkDone
destroy C

B --> A: Request Created
deactivate B

A --> User: Done
deactivate A

@enduml

@startuml
skinparam backgroundColor #EEEBDC
skinparam handwritten true

skinparam sequence {
ArrowColor DeepSkyBlue
ActorBorderColor DeepSkyBlue
LifeLineBorderColor blue
LifeLineBackgroundColor #A9DCDF

ParticipantBorderColor DeepSkyBlue
ParticipantBackgroundColor DodgerBlue
ParticipantFontName Impact
ParticipantFontSize 17
ParticipantFontColor #A9DCDF

ActorBackgroundColor aqua
ActorFontColor DeepSkyBlue
ActorFontSize 17
ActorFontName Aapex
}


_1.30 Changing padding 1 SEQUENCE DIAGRAM_

actor User
participant "First Class" as A
participant "Second Class" as B
participant "Last Class" as C

User -> A: DoWork
activate A

A -> B: Create Request
activate B

B -> C: DoWork
activate C
C --> B: WorkDone
destroy C

B --> A: Request Created
deactivate B

A --> User: Done
deactivate A

@enduml

### 1.30 Changing padding

It is possible to tune some padding settings.

@startuml
skinparam ParticipantPadding 20
skinparam BoxPadding 10

box "Foo1"
participant Alice1
participant Alice2
end box
box "Foo2"
participant Bob1


_1.30 Changing padding 1 SEQUENCE DIAGRAM_

participant Bob2
end box
Alice1 -> Bob1 : hello
Alice1 -> Out : out
@enduml


#### 2 USE CASE DIAGRAM

## 2 Use Case Diagram

Let's have few examples :

### 2.1 Usecases

Use cases are enclosed using between parentheses (because two parentheses looks like an oval).

You can also use theusecasekeyword to define a usecase. And you can define an alias, using theaskeyword.
This alias will be used latter, when defining relations.

@startuml

(First usecase)
(Another usecase) as (UC2)
usecase UC3
usecase (Last\nusecase) as UC4

@enduml

### 2.2 Actors

Actor are enclosed using between two points.

You can also use theactorkeyword to define an actor. And you can define an alias, using theaskeyword. This
alias will be used latter, when defining relations.

We will see later that the actor definitions are optional.

@startuml

:First Actor:
:Another\nactor: as Men2
actor Men3
actor :Last actor: as Men4

@enduml


_2.3 Usecases description 2 USE CASE DIAGRAM_

### 2.3 Usecases description

If you want to have description on several lines, you can use quotes.

You can also use the following separators:-- .. == __. And you can put titles within the separators.

@startuml

usecase UC1 as "You can use
several lines to define your usecase.
You can also use separators.
--
Several separators are possible.
==
And you can add titles:
..Conclusion..
This allows large description."

@enduml

### 2.4 Basic example

To link actors and use cases, the arrow-->is used.

The more dashes-in the arrow, the longer the arrow. You can add a label on the arrow, by adding a:character in
the arrow definition.

In this example, you see that _User_ has not been defined before, and is used as an actor.

@startuml

User -> (Start)
User --> (Use the application) : A small label

:Main Admin: ---> (Use the application) : This is\nyet another\nlabel

@enduml


_2.5 Extension 2 USE CASE DIAGRAM_

### 2.5 Extension

If one actor/use case extends another one, you can use the symbol<|--.

@startuml
:Main Admin: as Admin
(Use the application) as (Use)

User <|-- Admin
(Start) <|-- (Use)

@enduml

### 2.6 Using notes

You can use thenote left of,note right of,note top of,note bottom ofkeywords to define notes
related to a single object.

A note can be also define alone with thenotekeywords, then linked to other objects using the..symbol.

@startuml
:Main Admin: as Admin
(Use the application) as (Use)

User -> (Start)
User --> (Use)


_2.7 Stereotypes 2 USE CASE DIAGRAM_

Admin ---> (Use)

note right of Admin : This is an example.

note right of (Use)
A note can also
be on several lines
end note

note "This note is connected\nto several objects." as N2
(Start) .. N2
N2 .. (Use)
@enduml

### 2.7 Stereotypes

You can add stereotypes while defining actors and use cases using<<and>>.

@startuml
User << Human >>
:Main Database: as MySql << Application >>
(Start) << One Shot >>
(Use the application) as (Use) << Main >>

User -> (Start)
User --> (Use)

MySql --> (Use)

@enduml


_2.8 Changing arrows direction 2 USE CASE DIAGRAM_

### 2.8 Changing arrows direction

By default, links between classes have two dashes--and are vertically oriented. It is possible to use horizontal
link by putting a single dash (or dot) like this:

@startuml
:user: --> (Use case 1)
:user: -> (Use case 2)
@enduml

You can also change directions by reversing the link:

@startuml
(Use case 1) <.. :user:
(Use case 2) <- :user:
@enduml

It is also possible to change arrow direction by addingleft,right,upordownkeywords inside the arrow:

@startuml
:user: -left-> (dummyLeft)
:user: -right-> (dummyRight)
:user: -up-> (dummyUp)
:user: -down-> (dummyDown)
@enduml


_2.9 Splitting diagrams 2 USE CASE DIAGRAM_

You can shorten the arrow by using only the first character of the direction (for example,-d-instead of-down-)
or the two first characters (-do-).

Please note that you should not abuse this functionality : _Graphviz_ gives usually good results without tweaking.

### 2.9 Splitting diagrams

Thenewpagekeywords to split your diagram into several pages or images.

@startuml
:actor1: --> (Usecase1)
newpage
:actor2: --> (Usecase2)
@enduml

### 2.10 Left to right direction

The general default behavior when building diagram is **top to bottom**.

@startuml
'default
top to bottom direction
user1 --> (Usecase 1)
user2 --> (Usecase 2)

@enduml


_2.11 Skinparam 2 USE CASE DIAGRAM_

You may change to **left to right** using theleft to right directioncommand. The result is often better with
this direction.

@startuml

left to right direction
user1 --> (Usecase 1)
user2 --> (Usecase 2)

@enduml

### 2.11 Skinparam

You can use theskinparamcommand to change colors and fonts for the drawing.

You can use this command :

- In the diagram definition, like any other commands,
- In an included file,
- In a configuration file, provided in the command line or the ANT task.

You can define specific color and fonts for stereotyped actors and usecases.

@startuml
skinparam handwritten true

skinparam usecase {
BackgroundColor DarkSeaGreen
BorderColor DarkSlateGray

BackgroundColor<< Main >> YellowGreen
BorderColor<< Main >> YellowGreen

ArrowColor Olive
ActorBorderColor black
ActorFontName Courier

ActorBackgroundColor<< Human >> Gold


_2.12 Complete example 2 USE CASE DIAGRAM_

#### }

User << Human >>
:Main Database: as MySql << Application >>
(Start) << One Shot >>
(Use the application) as (Use) << Main >>

User -> (Start)
User --> (Use)

MySql --> (Use)

@enduml

### 2.12 Complete example

@startuml
left to right direction
skinparam packageStyle rectangle
actor customer
actor clerk
rectangle checkout {
customer -- (checkout)
(checkout) .> (payment) : include
(help) .> (checkout) : extends
(checkout) -- clerk
}
@enduml


#### 3 CLASS DIAGRAM

## 3 Class Diagram

### 3.1 Relations between classes

Relations between classes are defined using the following symbols :

```
Type Symbol Drawing
Extension <|--
Composition *--
Aggregation o--
```
It is possible to replace--by..to have a dotted line.

Knowing those rules, it is possible to draw the following drawings:

@startuml
Class01 <|-- Class02
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 -- Class10
@enduml

@startuml
Class11 <|.. Class12
Class13 --> Class14
Class15 ..> Class16
Class17 ..|> Class18
Class19 <--* Class20
@enduml

@startuml
Class21 #-- Class22
Class23 x-- Class24
Class25 }-- Class26
Class27 +-- Class28
Class29 ^-- Class30
@enduml


_3.2 Label on relations 3 CLASS DIAGRAM_

### 3.2 Label on relations

It is possible a add a label on the relation, using:, followed by the text of the label.

For cardinality, you can use double-quotes""on each side of the relation.

@startuml

Class01 "1" *-- "many" Class02 : contains

Class03 o-- Class04 : aggregation

Class05 --> "1" Class06

@enduml

You can add an extra arrow pointing at one object showing which object acts on the other object, using<or>at
the begin or at the end of the label.

@startuml
class Car

Driver - Car : drives >
Car *- Wheel : have 4 >
Car -- Person : < owns

@enduml


_3.3 Adding methods 3 CLASS DIAGRAM_

### 3.3 Adding methods

To declare fields and methods, you can use the symbol:followed by the field's or method's name.

The system checks for parenthesis to choose between methods and fields.

@startuml
Object <|-- ArrayList

Object : equals()
ArrayList : Object[] elementData
ArrayList : size()

@enduml

It is also possible to group between brackets{}all fields and methods.

Note that the syntax is highly flexible about type/name order.

@startuml
class Dummy {
String data
void methods()
}

class Flight {
flightNumber : Integer
departureTime : Date
}
@enduml

You can use{field}and{method}modifiers to override default behaviour of the parser about fields and methods.

@startuml
class Dummy {
{field} A field (despite parentheses)
{method} Some method
}

@enduml


_3.4 Defining visibility 3 CLASS DIAGRAM_

### 3.4 Defining visibility

When you define methods or fields, you can use characters to define the visibility of the corresponding item:

```
Character Icon for field Icon for method Visibility
```
- private
# protected
~ package private
+ public

@startuml

class Dummy {
-field1
#field2
~method1()
+method2()
}

@enduml

You can turn off this feature using theskinparam classAttributeIconSize 0command :

@startuml
skinparam classAttributeIconSize 0
class Dummy {
-field1
#field2
~method1()
+method2()
}

@enduml

### 3.5 Abstract and Static

You can define static or abstract methods or fields using the{static}or{abstract}modifier.

These modifiers can be used at the start or at the end of the line. You can also use{classifier}instead of
{static}.

@startuml
class Dummy {
{static} String id
{abstract} void methods()
}
@enduml


_3.6 Advanced class body 3 CLASS DIAGRAM_

### 3.6 Advanced class body

By default, methods and fields are automatically regrouped by PlantUML. You can use separators to define your
own way of ordering fields and methods. The following separators are possible :-- .. == __.

You can also use titles within the separators:

@startuml
class Foo1 {
You can use
several lines
..
as you want
and group
==
things together.
__
You can have as many groups
as you want
--
End of class
}

class User {
.. Simple Getter ..
+ getName()
+ getAddress()
.. Some setter ..
+ setName()
__ private data __
int age
-- encrypted --
String password
}

@enduml

### 3.7 Notes and stereotypes

Stereotypes are defined with theclasskeyword,<<and>>.

You can also define notes usingnote left of,note right of,note top of,note bottom ofkeywords.


_3.8 More on notes 3 CLASS DIAGRAM_

You can also define a note on the last defined class usingnote left,note right,note top,note bottom.

A note can be also define alone with thenotekeywords, then linked to other objects using the..symbol.

@startuml
class Object << general >>
Object <|--- ArrayList

note top of Object : In java, every class\nextends this one.

note "This is a floating note" as N1
note "This note is connected\nto several objects." as N2
Object .. N2
N2 .. ArrayList

class Foo
note left: On last defined class

@enduml

### 3.8 More on notes

It is also possible to use few html tags like :

- <b>
- <u>
- <i>
- <s>,<del>,<strike>
- <font color="#AAAAAA">or<font color="colorName">
- <color:#AAAAAA>or<color:colorName>
- <size:nn>to change font size
- <img src="file">or<img:file>: the file must be accessible by the filesystem

You can also have a note on several lines.

You can also define a note on the last defined class usingnote left,note right,note top,note bottom.


_3.9 Note on links 3 CLASS DIAGRAM_

@startuml

class Foo
note left: On last defined class

note top of Object
In java, <size:18>every</size> <u>class</u>
<b>extends</b>
<i>this</i> one.
end note

note as N1
This note is <u>also</u>
<b><color:royalBlue>on several</color>
<s>words</s> lines
And this is hosted by <img:sourceforge.jpg>
end note

@enduml

### 3.9 Note on links

It is possible to add a note on a link, just after the link definition, usingnote on link.

You can also usenote left on link,note right on link,note top on link,note bottom on link
if you want to change the relative position of the note with the label.

@startuml

class Dummy
Dummy --> Foo : A link
note on link #red: note that is red

Dummy --> Foo2 : Another link
note right on link #blue
this is my note on right link
and in blue
end note

@enduml


_3.10 Abstract class and interface 3 CLASS DIAGRAM_

### 3.10 Abstract class and interface

You can declare a class as abstract usingabstract"orabstract classkeywords.

The class will be printed in _italic_.

You can use theinterface,annotationandenumkeywords too.

@startuml

abstract class AbstractList
abstract AbstractCollection
interface List
interface Collection

List <|-- AbstractList
Collection <|-- AbstractCollection

Collection <|- List
AbstractCollection <|- AbstractList
AbstractList <|-- ArrayList

class ArrayList {
Object[] elementData
size()
}

enum TimeUnit {
DAYS
HOURS
MINUTES
}

annotation SuppressWarnings

@enduml


_3.11 Using non-letters 3 CLASS DIAGRAM_

### 3.11 Using non-letters

If you want to use non-letters in the class (or enum...) display, you can either :

- Use theaskeyword in the class definition
- Put quotes""around the class name

@startuml
class "This is my class" as class1
class class2 as "It works this way too"

class2 *-- "foo/dummy" : use
@enduml

### 3.12 Hide attributes, methods...

You can parameterize the display of classes using thehide/showcommand.

The basic command is:hide empty members. This command will hide attributes or methods if they are empty.

Instead ofempty members, you can use:

- empty fieldsorempty attributesfor empty fields,
- empty methodsfor empty methods,
- fieldsorattributeswhich will hide fields, even if they are described,
- methodswhich will hide methods, even if they are described,
- memberswhich will hide fields andmethods, even if they are described,
- circlefor the circled character in front of class name,


_3.13 Hide classes 3 CLASS DIAGRAM_

- stereotypefor the stereotype.

You can also provide, just after thehideorshowkeyword:

- classfor all classes,
- interfacefor all interfaces,
- enumfor all enums,
- <<foo1>>for classes which are stereotyped with _foo1_ ,
- an existing class name.

You can use severalshow/hidecommands to define rules and exceptions.

@startuml

class Dummy1 {
+myMethods()
}

class Dummy2 {
+hiddenMethod()
}

class Dummy3 <<Serializable>> {
String name
}

hide members
hide <<Serializable>> circle
show Dummy1 methods
show <<Serializable>> fields

@enduml

### 3.13 Hide classes

You can also use theshow/hidecommands to hide classes.

This may be useful if you define a large !included file, and if you want to hide come classes after file inclusion.

@startuml

class Foo1
class Foo2

Foo2 *-- Foo1

hide Foo2

@enduml


_3.14 Use generics 3 CLASS DIAGRAM_

### 3.14 Use generics

You can also use bracket<and>to define generics usage in a class.

@startuml

class Foo<? extends Element> {
int size()
}
Foo *- Element

@enduml

It is possible to disable this drawing usingskinparam genericDisplay oldcommand.

### 3.15 Specific Spot

Usually, a spotted character (C, I, E or A) is used for classes, interface, enum and abstract classes.

But you can define your own spot for a class when you define the stereotype, adding a single character and a color,
like in this example:

@startuml

class System << (S,#FF7700) Singleton >>
class Date << (D,orchid) >>
@enduml

### 3.16 Packages

You can define a package using thepackagekeyword, and optionally declare a background color for your package
(Using a html color code or name).

Note that package definitions can be nested.

@startuml

package "Classic Collections" #DDDDDD {
Object <|-- ArrayList
}


_3.17 Packages style 3 CLASS DIAGRAM_

package net.sourceforge.plantuml {
Object <|-- Demo1
Demo1 *- Demo2
}

@enduml

### 3.17 Packages style

There are different styles available for packages.

You can specify them either by setting a default style with the command :skinparam packageStyle, or by using
a stereotype on the package:

@startuml
scale 750 width
package foo1 <<Node>> {
class Class1
}

package foo2 <<Rectangle>> {
class Class2
}

package foo3 <<Folder>> {
class Class3
}

package foo4 <<Frame>> {
class Class4
}

package foo5 <<Cloud>> {
class Class5
}

package foo6 <<Database>> {
class Class6
}

@enduml


_3.18 Namespaces 3 CLASS DIAGRAM_

You can also define links between packages, like in the following example:

@startuml

skinparam packageStyle rectangle

package foo1.foo2 {
}

package foo1.foo2.foo3 {
class Object
}

foo1.foo2 +-- foo1.foo2.foo3

@enduml

### 3.18 Namespaces

In packages, the name of a class is the unique identifier of this class. It means that you cannot have two classes
with the very same name in different packages.

In that case, you should use namespaces instead of packages.

You can refer to classes from other namespaces by fully qualify them. Classes from the default namespace are
qualified with a starting dot.

Note that you don't have to explicitly create namespace : a fully qualified class is automatically put in the right
namespace.

@startuml

class BaseClass

namespace net.dummy #DDDDDD {
.BaseClass <|-- Person
Meeting o-- Person

.BaseClass <|- Meeting
}

namespace net.foo {


_3.19 Automatic namespace creation 3 CLASS DIAGRAM_

```
net.dummy.Person <|- Person
.BaseClass <|-- Person
```
net.dummy.Meeting o-- Person
}

BaseClass <|-- net.unused.Person

@enduml

### 3.19 Automatic namespace creation

You can define another separator (other than the dot) using the command :set namespaceSeparator ???.

@startuml

set namespaceSeparator ::
class X1::X2::foo {
some info
}

@enduml

You can disable automatic package creation using the commandset namespaceSeparator none.

@startuml

set namespaceSeparator none
class X1.X2.foo {
some info
}

@enduml


_3.20 Lollipop interface 3 CLASS DIAGRAM_

### 3.20 Lollipop interface

You can also define lollipops interface on classes, using the following syntax:

- bar ()- foo
- bar ()-- foo
- foo -() bar

@startuml
class foo
bar ()- foo
@enduml

### 3.21 Changing arrows direction

By default, links between classes have two dashes--and are vertically oriented. It is possible to use horizontal
link by putting a single dash (or dot) like this:

@startuml
Room o- Student
Room *-- Chair
@enduml

You can also change directions by reversing the link:

@startuml
Student -o Room
Chair --* Room
@enduml

It is also possible to change arrow direction by addingleft,right,upordownkeywords inside the arrow:

@startuml
foo -left-> dummyLeft
foo -right-> dummyRight
foo -up-> dummyUp
foo -down-> dummyDown
@enduml


_3.22 Association classes 3 CLASS DIAGRAM_

You can shorten the arrow by using only the first character of the direction (for example,-d-instead of-down-)
or the two first characters (-do-).

Please note that you should not abuse this functionality : _Graphviz_ gives usually good results without tweaking.

### 3.22 Association classes

You can define _association class_ after that a relation has been defined between two classes, like in this example:

@startuml
class Student {
Name
}
Student "0..*" - "1..*" Course
(Student, Course) .. Enrollment

class Enrollment {
drop()
cancel()
}
@enduml

You can define it in another direction:

@startuml
class Student {
Name
}
Student "0..*" -- "1..*" Course
(Student, Course). Enrollment

class Enrollment {
drop()
cancel()


_3.23 Skinparam 3 CLASS DIAGRAM_

#### }

@enduml

### 3.23 Skinparam

You can use theskinparamcommand to change colors and fonts for the drawing.

You can use this command :

- In the diagram definition, like any other commands,
- In an included file,
- In a configuration file, provided in the command line or the ANT task.

@startuml

skinparam class {
BackgroundColor PaleGreen
ArrowColor SeaGreen
BorderColor SpringGreen
}
skinparam stereotypeCBackgroundColor YellowGreen

Class01 "1" *-- "many" Class02 : contains

Class03 o-- Class04 : aggregation

@enduml

### 3.24 Skinned Stereotypes

You can define specific color and fonts for stereotyped classes.


_3.25 Color gradient 3 CLASS DIAGRAM_

@startuml

skinparam class {
BackgroundColor PaleGreen
ArrowColor SeaGreen
BorderColor SpringGreen
BackgroundColor<<Foo>> Wheat
BorderColor<<Foo>> Tomato
}
skinparam stereotypeCBackgroundColor YellowGreen
skinparam stereotypeCBackgroundColor<< Foo >> DimGray

Class01 <<Foo>>
Class03 <<Foo>>
Class01 "1" *-- "many" Class02 : contains

Class03 o-- Class04 : aggregation

@enduml

### 3.25 Color gradient

It's possible to declare individual color for classes or note using the # notation.

You can use either standard color name or RGB code.

You can also use color gradient in background, with the following syntax: two colors names separated either by:

- |,
- /,
- \,
- or-

depending the direction of the gradient.

For example, you could have:

@startuml

skinparam backgroundcolor AntiqueWhite/Gold
skinparam classBackgroundColor Wheat|CornflowerBlue

class Foo #red-green
note left of Foo #blue\9932CC
this is my
note on this class
end note

package example #GreenYellow/LightGoldenRodYellow {


_3.26 Help on layout 3 CLASS DIAGRAM_

class Dummy
}

@enduml

### 3.26 Help on layout

Sometimes, the default layout is not perfect...

You can usetogetherkeyword to group some classes together : the layout engine will try to group them (as if
they were in the same package).

You can also usehiddenlinks to force the layout.

@startuml

class Bar1
class Bar2
together {
class Together1
class Together2
class Together3
}
Together1 - Together2
Together2 - Together3
Together2 -[hidden]--> Bar1
Bar1 -[hidden]> Bar2

@enduml

### 3.27 Splitting large files

Sometimes, you will get some very large image files.

You can use thepage (hpages)x(vpages)command to split the generated image into several files :

hpagesis a number that indicated the number of horizontal pages, andvpagesis a number that indicated the
number of vertical pages.


_3.27 Splitting large files 3 CLASS DIAGRAM_

You can also use some specific skinparam settings to put borders on splitted pages (see example).

@startuml
' Split into 4 pages
page 2x2
skinparam pageMargin 10
skinparam pageExternalColor gray
skinparam pageBorderColor black

class BaseClass

namespace net.dummy #DDDDDD {
.BaseClass <|-- Person
Meeting o-- Person

.BaseClass <|- Meeting

}

namespace net.foo {
net.dummy.Person <|- Person
.BaseClass <|-- Person

net.dummy.Meeting o-- Person
}

BaseClass <|-- net.unused.Person
@enduml


#### 4 ACTIVITY DIAGRAM

## 4 Activity Diagram

### 4.1 Simple Activity

You can use(*)for the starting point and ending point of the activity diagram.

In some occasion, you may want to use(*top)to force the starting point to be at the top of the diagram.

Use-->for arrows.

@startuml

(*) --> "First Activity"
"First Activity" --> (*)

@enduml

### 4.2 Label on arrows

By default, an arrow starts at the last used activity.

You can put a label on an arrow using brackets[and]just after the arrow definition.

@startuml

(*) --> "First Activity"
-->[You can put also labels] "Second Activity"
--> (*)

@enduml

### 4.3 Changing arrow direction

You can use->for horizontal arrows. It is possible to force arrow's direction using the following syntax:

- -down->(default arrow)
- -right->or->


_4.4 Branches 4 ACTIVITY DIAGRAM_

- -left->
- -up->

@startuml

(*) -up-> "First Activity"
-right-> "Second Activity"
--> "Third Activity"
-left-> (*)

@enduml

### 4.4 Branches

You can useif/then/elsekeywords to define branches.

@startuml
(*) --> "Initialization"

if "Some Test" then
-->[true] "Some Activity"
--> "Another activity"
-right-> (*)
else
->[false] "Something else"
-->[Ending process] (*)
endif

@enduml

Unfortunately, you will have to sometimes repeat the same activity in the diagram text:

@startuml
(*) --> "check input"


_4.5 More on Branches 4 ACTIVITY DIAGRAM_

If "input is verbose" then
--> [Yes] "turn on verbosity"
--> "run command"
else
--> "run command"
Endif
-->(*)
@enduml

### 4.5 More on Branches

By default, a branch is connected to the last defined activity, but it is possible to override this and to define a link
with theifkeywords.

It is also possible to nest branches.

@startuml

(*) --> if "Some Test" then

```
-->[true] "activity 1"
```
if "" then
-> "activity 3" as a3
else
if "Other test" then
-left-> "activity 5"
else
--> "activity 6"
endif
endif

else

```
->[false] "activity 2"
```
endif


_4.6 Synchronization 4 ACTIVITY DIAGRAM_

a3 --> if "last test" then
--> "activity 7"
else
-> "activity 8"
endif

@enduml

### 4.6 Synchronization

You can use=== code ===to display synchronization bars.

@startuml

(*) --> ===B1===
--> "Parallel Activity 1"
--> ===B2===

===B1=== --> "Parallel Activity 2"
--> ===B2===

--> (*)

@enduml


_4.7 Long activity description 4 ACTIVITY DIAGRAM_

### 4.7 Long activity description

When you declare activities, you can span on several lines the description text. You can also add\nin the descrip-
tion.

You can also give a short code to the activity with theaskeyword. This code can be used latter in the diagram
description.

@startuml
(*) -left-> "this <size:20>activity</size>
is <b>very</b> <color:red>long2</color>
and defined on several lines
that contains many <i>text</i>" as A1

-up-> "Another activity\n on several lines"

A1 --> "Short activity <img:sourceforge.jpg>"
@enduml

### 4.8 Notes

You can add notes on a activity using the commandsnote left,note right,note topornote bottom, just
after the description of the activity you want to note.

If you want to put a note on the starting point, define the note at the very beginning of the diagram description.

You can also have a note on several lines, using theendnotekeywords.

@startuml


_4.9 Partition 4 ACTIVITY DIAGRAM_

(*) --> "Some Activity"
note right: This activity has to be defined
"Some Activity" --> (*)
note left
This note is on
several lines
end note

@enduml

### 4.9 Partition

You can define a partition using thepartitionkeyword, and optionally declare a background color for your
partition (Using a html color code or name)

When you declare activities, they are automatically put in the last used partition.

You can close the partition definition using a closing bracket}.

@startuml

partition Conductor {
(*) --> "Climbs on Platform"
--> === S1 ===
--> Bows
}

partition Audience #LightSkyBlue {
=== S1 === --> Applauds
}

partition Conductor {
Bows --> === S2 ===
--> WavesArmes
Applauds --> === S2 ===
}

partition Orchestra #CCCCEE {
WavesArmes --> Introduction
--> "Play music"
}

@enduml


_4.10 Skinparam 4 ACTIVITY DIAGRAM_

### 4.10 Skinparam

You can use theskinparamcommand to change colors and fonts for the drawing.

You can use this command :

- In the diagram definition, like any other commands,
- In an included file,
- In a configuration file, provided in the command line or the ANT task.

You can define specific color and fonts for stereotyped activities.

@startuml

skinparam backgroundColor #AAFFFF
skinparam activity {
StartColor red
BarColor SaddleBrown
EndColor Silver
BackgroundColor Peru
BackgroundColor<< Begin >> Olive
BorderColor Peru
FontName Impact
}

(*) --> "Climbs on Platform" << Begin >>


_4.11 Octagon 4 ACTIVITY DIAGRAM_

#### --> === S1 ===

--> Bows
--> === S2 ===
--> WavesArmes
--> (*)

@enduml

### 4.11 Octagon

You can change the shape of activities to octagon using theskinparam activityShape octagoncommand.

@startuml
'Default is skinparam activityShape roundBox
skinparam activityShape octagon

(*) --> "First Activity"
"First Activity" --> (*)

@enduml

### 4.12 Complete example

@startuml
title Servlet Container

(*) --> "ClickServlet.handleRequest()"


_4.12 Complete example 4 ACTIVITY DIAGRAM_

--> "new Page"

if "Page.onSecurityCheck" then
->[true] "Page.onInit()"

```
if "isForward?" then
->[no] "Process controls"
```
```
if "continue processing?" then
-->[yes] ===RENDERING===
else
-->[no] ===REDIRECT_CHECK===
endif
```
```
else
-->[yes] ===RENDERING===
endif
```
if "is Post?" then
-->[yes] "Page.onPost()"
--> "Page.onRender()" as render
--> ===REDIRECT_CHECK===
else
-->[no] "Page.onGet()"
--> render
endif

else
-->[false] ===REDIRECT_CHECK===
endif

if "Do redirect?" then
->[yes] "redirect request"
--> ==BEFORE_DESTROY===
else
if "Do Forward?" then
-left->[yes] "Forward request"
--> ==BEFORE_DESTROY===
else
-right->[no] "Render page template"
--> ==BEFORE_DESTROY===
endif
endif

--> "Page.onDestroy()"
-->(*)

@enduml


_4.12 Complete example 4 ACTIVITY DIAGRAM_


#### 5 ACTIVITY DIAGRAM (BETA)

## 5 Activity Diagram (beta)

Current syntax for activity diagram has several limitations and drawbacks (for example, it's difficult to maintain).

So a completely new syntax and implementation is proposed as **betaversion** to users (starting with V7947), so that
we could define a better format and syntax.

Another advantage of this new implementation is that it's done without the need of having Graphviz installed (as
for sequence diagrams).

The new syntax will replace the old one. However, for compatibility reason, the old syntax will still be recognized,
to ensure _ascending compatibility_.

Users are simply encouraged to migrate to the new syntax.

### 5.1 Simple Activity

Activities label starts with:and ends with;.

Text formatting can be done using creole wiki syntax.

They are implicitly linked in their definition order.

@startuml
:Hello world;
:This is defined on
several **lines**;
@enduml

### 5.2 Start/Stop

You can usestartandstopkeywords to denote the beginning and the end of a diagram.

@startuml
start
:Hello world;
:This is defined on
several **lines**;
stop
@enduml

You can also use theendkeyword.


_5.3 Conditional 5 ACTIVITY DIAGRAM (BETA)_

@startuml
start
:Hello world;
:This is defined on
several **lines**;
end
@enduml

### 5.3 Conditional

You can useif,thenandelsekeywords to put tests if your diagram. Labels can be provided using parentheses.

@startuml

start

if (Graphviz installed?) then (yes)
:process all\ndiagrams;
else (no)
:process only
__sequence__ and __activity__ diagrams;
endif

stop

@enduml

You can use theelseifkeyword to have several tests :

@startuml
start
if (condition A) then (yes)
:Text 1;
elseif (condition B) then (yes)
:Text 2;
stop
elseif (condition C) then (yes)


_5.4 Repeat loop 5 ACTIVITY DIAGRAM (BETA)_

:Text 3;
elseif (condition D) then (yes)
:Text 4;
else (nothing)
:Text else;
endif
stop
@enduml

### 5.4 Repeat loop

You can userepeatandrepeatwhilekeywords to have repeat loops.

@startuml

start

repeat
:read data;
:generate diagrams;
repeat while (more data?) is (yes)
->no;
stop

@enduml


_5.5 While loop 5 ACTIVITY DIAGRAM (BETA)_

### 5.5 While loop

You can usewhileandend whilekeywords to have repeat loops.

@startuml

start

while (data available?)
:read data;
:generate diagrams;
endwhile

stop

@enduml

It is possible to provide a label after theendwhilekeyword, or using theiskeyword.

@startuml
while (check filesize ?) is (not empty)
:read file;
endwhile (empty)
:close file;
@enduml

### 5.6 Parallel processing

You can usefork,fork againandend forkkeywords to denote parallel processing.

@startuml

start

if (multiprocessor?) then (yes)
fork
:Treatment 1;
fork again


_5.7 Notes 5 ACTIVITY DIAGRAM (BETA)_

:Treatment 2;
end fork
else (monoproc)
:Treatment 1;
:Treatment 2;
endif

@enduml

### 5.7 Notes

Text formatting can be done using creole wiki syntax.

A note can be floating, usingfloatingkeyword.

@startuml

start
:foo1;
floating note left: This is a note
:foo2;
note right
This note is on several
//lines// and can
contain <b>HTML</b>
====
* Calling the method ""foo()"" is prohibited
end note
stop

@enduml


_5.8 Colors 5 ACTIVITY DIAGRAM (BETA)_

### 5.8 Colors

You can specify a color for some activities.

@startuml

start
:starting progress;
#HotPink:reading configuration files
These files should be edited at this point!;
#AAAAAA:ending of the process;

@enduml

### 5.9 Arrows

Using the->notation, you can add texts to arrow, and change their color.

It's also possible to have dotted, dashed, bold or hidden arrows.

@startuml
:foo1;
-> You can put text on arrows;
if (test) then
-[#blue]->
:foo2;
-[#green,dashed]-> The text can
also be on several lines
and **very** long...;
:foo3;
else
-[#black,dotted]->
:foo4;
endif
-[#gray,bold]->
:foo5;
@enduml


_5.10 Connector 5 ACTIVITY DIAGRAM (BETA)_

### 5.10 Connector

You can use parentheses to denote connector.

@startuml
start
:Some activity;
(A)
detach
(A)
:Other activity;
@enduml

### 5.11 Grouping

You can group activity together by defining partition:

@startuml
start
partition Initialization {
:read config file;
:init internal variable;
}
partition Running {
:wait for user interaction;
:print information;
}


_5.12 Swimlanes 5 ACTIVITY DIAGRAM (BETA)_

stop
@enduml

### 5.12 Swimlanes

Using pipe|, you can define swimlanes.

It's also possible to change swimlanes color.

@startuml
|Swimlane1|
start
:foo1;
|#AntiqueWhite|Swimlane2|
:foo2;
:foo3;
|Swimlane1|
:foo4;
|Swimlane2|
:foo5;
stop
@enduml


_5.13 Detach 5 ACTIVITY DIAGRAM (BETA)_

### 5.13 Detach

It's possible to remove an arrow using thedetachkeyword.

@startuml
:start;
fork
:foo1;
:foo2;
fork again
:foo3;
detach
endfork
if (foo4) then
:foo5;
detach
endif
:foo6;
detach
:foo7;
stop
@enduml


#### 5.14 SDL 5 ACTIVITY DIAGRAM (BETA)

### 5.14 SDL

By changing the final;separator, you can set different rendering for the activity:

- |
- <
- >
- /
- ]
- }

@startuml
:Ready;
:next(o)|
:Receiving;
split
:nak(i)<
:ack(o)>
split again
:ack(i)<
:next(o)
on several lines|
:i := i + 1]
:ack(o)>
split again
:err(i)<
:nak(o)>
split again
:foo/
split again
:i > 5}


_5.15 Complete example 5 ACTIVITY DIAGRAM (BETA)_

stop
end split
:finish;
@enduml

### 5.15 Complete example

@startuml

start
:ClickServlet.handleRequest();
:new page;
if (Page.onSecurityCheck) then (true)
:Page.onInit();
if (isForward?) then (no)
:Process controls;
if (continue processing?) then (no)
stop
endif

if (isPost?) then (yes)
:Page.onPost();
else (no)
:Page.onGet();
endif
:Page.onRender();
endif
else (false)
endif

if (do redirect?) then (yes)


_5.15 Complete example 5 ACTIVITY DIAGRAM (BETA)_

:redirect process;
else
if (do forward?) then (yes)
:Forward request;
else (no)
:Render page template;
endif
endif

stop

@enduml


#### 6 COMPONENT DIAGRAM

## 6 Component Diagram

Let's have few examples :

### 6.1 Components

Components must be bracketed.

You can also use thecomponentkeyword to define a component. And you can define an alias, using theas
keyword. This alias will be used latter, when defining relations.

@startuml

[First component]
[Another component] as Comp2
component Comp3
component [Last\ncomponent] as Comp4

@enduml

### 6.2 Interfaces

Interface can be defined using the()symbol (because this looks like a circle).

You can also use theinterfacekeyword to define an interface. And you can define an alias, using theaskeyword.
This alias will be used latter, when defining relations.

We will see latter that interface definition is optional.

@startuml

() "First Interface"
() "Another interface" as Interf2
interface Interf3
interface "Last\ninterface" as Interf4

@enduml


_6.3 Basic example 6 COMPONENT DIAGRAM_

### 6.3 Basic example

Links between elements are made using combinations of dotted line (..), straight line (--), and arrows (-->)
symbols.

@startuml

DataAccess - [First Component]
[First Component] ..> HTTP : use

@enduml

### 6.4 Using notes

You can use thenote left of,note right of,note top of,note bottom ofkeywords to define notes
related to a single object.

A note can be also define alone with thenotekeywords, then linked to other objects using the..symbol.

@startuml

interface "Data Access" as DA

DA - [First Component]
[First Component] ..> HTTP : use

note left of HTTP : Web Service only

note right of [First Component]
A note can also
be on several lines
end note

@enduml

### 6.5 Grouping Components

You can use several keywords to group components and interfaces together:


_6.5 Grouping Components 6 COMPONENT DIAGRAM_

- package
- node
- folder
- frame
- cloud
- database

@startuml

package "Some Group" {
HTTP - [First Component]
[Another Component]
}

node "Other Groups" {
FTP - [Second Component]
[First Component] --> FTP
}

cloud {
[Example 1]
}

database "MySql" {
folder "This is my folder" {
[Folder 3]
}
frame "Foo" {
[Frame 4]
}
}

[Another Component] --> [Example 1]
[Example 1] --> [Folder 3]
[Folder 3] --> [Frame 4]

@enduml


_6.6 Changing arrows direction 6 COMPONENT DIAGRAM_

### 6.6 Changing arrows direction

By default, links between classes have two dashes--and are vertically oriented. It is possible to use horizontal
link by putting a single dash (or dot) like this:

@startuml
[Component] --> Interface1
[Component] -> Interface2
@enduml

You can also change directions by reversing the link:

@startuml
Interface1 <-- [Component]
Interface2 <- [Component]
@enduml


_6.7 Use UML2 notation 6 COMPONENT DIAGRAM_

It is also possible to change arrow direction by addingleft,right,upordownkeywords inside the arrow:

@startuml
[Component] -left-> left
[Component] -right-> right
[Component] -up-> up
[Component] -down-> down
@enduml

You can shorten the arrow by using only the first character of the direction (for example,-d-instead of-down-)
or the two first characters (-do-).

Please note that you should not abuse this functionality : _Graphviz_ gives usually good results without tweaking.

### 6.7 Use UML2 notation

Theskinparam componentStyle uml2command is used to switch to UML2 notation.

@startuml
skinparam componentStyle uml2

interface "Data Access" as DA

DA - [First Component]
[First Component] ..> HTTP : use

@enduml


_6.8 Long description 6 COMPONENT DIAGRAM_

### 6.8 Long description

It is possible to put description on several lines using square brackets.

@startuml
component comp1 [
This component
has a long comment
on several lines
]
@enduml

### 6.9 Individual colors

You can specify a color after component definition.

@startuml
component [Web Server] #Yellow
@enduml

### 6.10 Using Sprite in Stereotype

You can use sprites within stereotype components.

@startuml
sprite $businessProcess [16x16/16] {
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFF0FFFFF
FFFFFFFFFF00FFFF
FF00000000000FFF
FF000000000000FF
FF00000000000FFF
FFFFFFFFFF00FFFF
FFFFFFFFFF0FFFFF


_6.11 Skinparam 6 COMPONENT DIAGRAM_

#### FFFFFFFFFFFFFFFF

#### FFFFFFFFFFFFFFFF

#### FFFFFFFFFFFFFFFF

#### FFFFFFFFFFFFFFFF

#### FFFFFFFFFFFFFFFF

#### }

rectangle " End to End\nbusiness process" <<$businessProcess>> {
rectangle "inner process 1" <<$businessProcess>> as src
rectangle "inner process 2" <<$businessProcess>> as tgt
src -> tgt
}
@enduml

### 6.11 Skinparam

You can use theskinparamcommand to change colors and fonts for the drawing.

You can use this command :

- In the diagram definition, like any other commands,
- In an included file,
- In a configuration file, provided in the command line or the ANT task.

You can define specific color and fonts for stereotyped components and interfaces.

@startuml

skinparam interface {
backgroundColor RosyBrown
borderColor orange
}

skinparam component {
FontSize 13
BackgroundColor<<Apache>> Red
BorderColor<<Apache>> #FF6655
FontName Courier
BorderColor black
BackgroundColor gold
ArrowFontName Impact
ArrowColor #FF6655
ArrowFontColor #777777
}

() "Data Access" as DA

DA - [First Component]
[First Component] ..> () HTTP : use


_6.11 Skinparam 6 COMPONENT DIAGRAM_

HTTP - [Web Server] << Apache >>

@enduml

@startuml
[AA] <<static lib>>
[BB] <<shared lib>>
[CC] <<static lib>>

node node1
node node2 <<shared node>>
database Production

skinparam component {
backgroundColor<<static lib>> DarkKhaki
backgroundColor<<shared lib>> Green
}

skinparam node {
borderColor Green
backgroundColor Yellow
backgroundColor<<shared node>> Magenta
}
skinparam databaseBackgroundColor Aqua

@enduml


#### 7 STATE DIAGRAM

## 7 State Diagram

State diagrams are used to give an abstract description of the behavior of a system. This behavior is represented as
a series of events that can occur in one or more possible states.

### 7.1 Simple State

You can use[*]for the starting point and ending point of the state diagram.

Use-->for arrows.

@startuml

[*] --> State1
State1 --> [*]
State1 : this is a string
State1 : this is another string

State1 -> State2
State2 --> [*]

@enduml

### 7.2 Change state rendering

You can usehide empty descriptionto render state as simple box.

@startuml
hide empty description
[*] --> State1
State1 --> [*]
State1 : this is a string
State1 : this is another string

State1 -> State2
State2 --> [*]
@enduml


_7.3 Composite state 7 STATE DIAGRAM_

### 7.3 Composite state

A state can also be composite. You have to define it using thestatekeywords and brackets.

@startuml
scale 350 width
[*] --> NotShooting

state NotShooting {
[*] --> Idle
Idle --> Configuring : EvConfig
Configuring --> Idle : EvConfig
}

state Configuring {
[*] --> NewValueSelection
NewValueSelection --> NewValuePreview : EvNewValue
NewValuePreview --> NewValueSelection : EvNewValueRejected
NewValuePreview --> NewValueSelection : EvNewValueSaved

```
state NewValuePreview {
State1 -> State2
}
```
}
@enduml


_7.4 Long name 7 STATE DIAGRAM_

### 7.4 Long name

You can also use thestatekeyword to use long description for states.

@startuml
scale 600 width

[*] -> State1
State1 --> State2 : Succeeded
State1 --> [*] : Aborted
State2 --> State3 : Succeeded
State2 --> [*] : Aborted
state State3 {
state "Accumulate Enough Data\nLong State Name" as long1
long1 : Just a test
[*] --> long1
long1 --> long1 : New Data
long1 --> ProcessData : Enough Data
}
State3 --> State3 : Failed
State3 --> [*] : Succeeded / Save Result
State3 --> [*] : Aborted

@enduml


_7.5 Fork 7 STATE DIAGRAM_

### 7.5 Fork

You can also fork and join using the<<fork>>and<<join>>stereotypes.

@startuml

state fork_state <<fork>>
[*] --> fork_state
fork_state --> State2
fork_state --> State3

state join_state <<join>>
State2 --> join_state
State3 --> join_state
join_state --> State4
State4 --> [*]

@enduml


_7.6 Concurrent state 7 STATE DIAGRAM_

### 7.6 Concurrent state

You can define concurrent state into a composite state using either--or||symbol as separator.

@startuml
[*] --> Active

state Active {
[*] -> NumLockOff
NumLockOff --> NumLockOn : EvNumLockPressed
NumLockOn --> NumLockOff : EvNumLockPressed
--
[*] -> CapsLockOff
CapsLockOff --> CapsLockOn : EvCapsLockPressed
CapsLockOn --> CapsLockOff : EvCapsLockPressed
--
[*] -> ScrollLockOff
ScrollLockOff --> ScrollLockOn : EvCapsLockPressed
ScrollLockOn --> ScrollLockOff : EvCapsLockPressed
}

@enduml


_7.7 Arrow direction 7 STATE DIAGRAM_

### 7.7 Arrow direction

You can use->for horizontal arrows. It is possible to force arrow's direction using the following syntax:

- -down->(default arrow)
- -right->or->
- -left->
- -up->

@startuml

[*] -up-> First
First -right-> Second
Second --> Third
Third -left-> Last

@enduml


_7.8 Note 7 STATE DIAGRAM_

You can shorten the arrow by using only the first character of the direction (for example,-d-instead of-down-)
or the two first characters (-do-).

Please note that you should not abuse this functionality : _Graphviz_ gives usually good results without tweaking.

### 7.8 Note

You can also define notes usingnote left of,note right of,note top of,note bottom ofkeywords.

You can also define notes on several lines.

@startuml

[*] --> Active
Active --> Inactive

note left of Active : this is a short\nnote

note right of Inactive
A note can also
be defined on
several lines
end note

@enduml

You can also have floating notes.

@startuml

state foo
note "This is a floating note" as N1

@enduml


_7.9 More in notes 7 STATE DIAGRAM_

### 7.9 More in notes

You can put notes on composite states.

@startuml

[*] --> NotShooting

state "Not Shooting State" as NotShooting {
state "Idle mode" as Idle
state "Configuring mode" as Configuring
[*] --> Idle
Idle --> Configuring : EvConfig
Configuring --> Idle : EvConfig
}

note right of NotShooting : This is a note on a composite state

@enduml

### 7.10 Skinparam

You can use theskinparamcommand to change colors and fonts for the drawing.

You can use this command :

- In the diagram definition, like any other commands,
- In an included file,
- In a configuration file, provided in the command line or the ANT task.

You can define specific color and fonts for stereotyped states.

@startuml
skinparam backgroundColor LightYellow
skinparam state {
StartColor MediumBlue


_7.10 Skinparam 7 STATE DIAGRAM_

EndColor Red
BackgroundColor Peru
BackgroundColor<<Warning>> Olive
BorderColor Gray
FontName Impact
}

[*] --> NotShooting

state "Not Shooting State" as NotShooting {
state "Idle mode" as Idle <<Warning>>
state "Configuring mode" as Configuring
[*] --> Idle
Idle --> Configuring : EvConfig
Configuring --> Idle : EvConfig
}

NotShooting --> [*]
@enduml


#### 8 OBJECT DIAGRAM

## 8 Object Diagram

### 8.1 Definition of objects

You define instance of objects using theobjectkeywords.

@startuml
object firstObject
object "My Second Object" as o2
@enduml

### 8.2 Relations between objects

Relations between objects are defined using the following symbols :

```
Type Symbol Image
Extension <|--
Composition *--
Aggregation o--
```
It is possible to replace--by..to have a dotted line.

Knowing those rules, it is possible to draw the following drawings.

It is possible a add a label on the relation, using:followed by the text of the label.

For cardinality, you can use double-quotes""on each side of the relation.

@startuml
object Object01
object Object02
object Object03
object Object04
object Object05
object Object06
object Object07
object Object08

Object01 <|-- Object02
Object03 *-- Object04
Object05 o-- "4" Object06
Object07 .. Object08 : some labels
@enduml

### 8.3 Adding fields

To declare fields, you can use the symbol:followed by the field's name.


_8.4 Common features with class diagrams 8 OBJECT DIAGRAM_

@startuml

object user

user : name = "Dummy"
user : id = 123

@enduml

It is also possible to group all fields between brackets{}.

@startuml

object user {
name = "Dummy"
id = 123
}

@enduml

### 8.4 Common features with class diagrams

- Hide attributes, methods...
- Defines notes
- Use packages
- Skin the output


#### 9 TIMING DIAGRAM

## 9 Timing Diagram

This is only a proposal and subject to change.

You are very welcome to create a new discussion on this future syntax. Your feedbacks, ideas and suggestions help
us to find the right solution.

### 9.1 Declaring participant

You declare participant usingconciseorrobustkeyword, depending on how you want them to be drawn.

You define state change using the@notation, and theisverb.

@startuml
robust "Web Browser" as WB
concise "Web User" as WU

@0
WU is Idle
WB is Idle

@100
WU is Waiting
WB is Processing

@300
WB is Waiting
@enduml

### 9.2 Adding message

You can add message using the following syntax.

@startuml
robust "Web Browser" as WB
concise "Web User" as WU

@0
WU is Idle
WB is Idle

@100
WU -> WB : URL
WU is Waiting
WB is Processing

@300
WB is Waiting


_9.3 Relative time 9 TIMING DIAGRAM_

@enduml

### 9.3 Relative time

It is possible to use relative time with@.

@startuml
robust "DNS Resolver" as DNS
robust "Web Browser" as WB
concise "Web User" as WU

@0
WU is Idle
WB is Idle
DNS is Idle

@+100
WU -> WB : URL
WU is Waiting
WB is Processing

@+200
WB is Waiting
WB -> DNS@+50 : Resolve URL

@+100
DNS is Processing

@+300
DNS is Idle
@enduml


_9.4 Participant oriented 9 TIMING DIAGRAM_

### 9.4 Participant oriented

Rather than declare the diagram in chronological order, you can define it by participant.

@startuml
robust "Web Browser" as WB
concise "Web User" as WU

@WB
0 is idle
+200 is Proc.
+100 is Waiting

@WU
0 is Waiting
+500 is ok
@enduml

### 9.5 Setting scale

You can also set a specific scale.

@startuml
concise "Web User" as WU
scale 100 as 50 pixels

@WU
0 is Waiting
+500 is ok
@enduml

### 9.6 Initial state

You can also define an inital state.

@startuml
robust "Web Browser" as WB
concise "Web User" as WU

WB is Initializing
WU is Absent


_9.7 Intricated state 9 TIMING DIAGRAM_

#### @WB

0 is idle
+200 is Processing
+100 is Waiting

@WU
0 is Waiting
+500 is ok
@enduml

### 9.7 Intricated state

A signal could be in some undefined state.

@startuml
robust "Signal1" as S1
robust "Signal2" as S2
S1 has 0,1,2,hello
S2 has 0,1,2
@0
S1 is 0
S2 is 0
@100
S1 is {0,1} #SlateGrey
S2 is {0,1}
@200
S1 is 1
S2 is 0
@300
S1 is hello
S2 is {0,2}
@enduml


_9.8 Hidden state 9 TIMING DIAGRAM_

### 9.8 Hidden state

It is also possible to hide some state.

@startuml
concise "Web User" as WU

@0
WU is {-}

@100
WU is A1

@200
WU is {-}

@300
WU is {hidden}

@400
WU is A3

@500
WU is {-}
@enduml

### 9.9 Adding constraint

It is possible to display time constraints on the diagrams.

@startuml
robust "Web Browser" as WB
concise "Web User" as WU

WB is Initializing
WU is Absent

@WB
0 is idle
+200 is Processing
+100 is Waiting
WB@0 <-> @50 : {50 ms lag}

@WU
0 is Waiting
+500 is ok
@200 <-> @+150 : {150 ms}
@enduml


_9.10 Adding texts 9 TIMING DIAGRAM_

### 9.10 Adding texts

You can optionally add a title, a header, a footer, a legend and a caption:

@startuml
Title This is my title
header: some header
footer: some footer
legend
Some legend
end legend
caption some caption

robust "Web Browser" as WB
concise "Web User" as WU

@0
WU is Idle
WB is Idle

@100
WU is Waiting
WB is Processing

@300
WB is Waiting
@enduml


#### 10 GANTT DIAGRAM

## 10 Gantt Diagram

This is only a proposal and subject to change.

You are very welcome to create a new discussion on this future syntax. Your feedbacks, ideas and suggestions help
us to find the right solution.

The Gantt is described in _natural_ language, using very simple sentences (subject-verb-complement).

### 10.1 Declaring tasks

Tasks defined using square bracket. Their durations are defined using thelastverb:

@startgantt
[Prototype design] lasts 15 days
[Test prototype] lasts 10 days
@endgantt

### 10.2 Adding constraints

It is possible to add constraints between task.

@startgantt
[Prototype design] lasts 15 days
[Test prototype] lasts 10 days
[Test prototype] starts at [Prototype design]'s end
@endgantt

@startgantt
[Prototype design] lasts 10 days
[Code prototype] lasts 10 days
[Write tests] lasts 5 days
[Code prototype] starts at [Prototype design]'s end
[Write tests] starts at [Code prototype]'s start
@endgantt

### 10.3 Short names

It is possible to define short name for tasks with theaskeyword.

@startgantt
[Prototype design] as [D] lasts 15 days
[Test prototype] as [T] lasts 10 days
[T] starts at [D]'s end
@endgantt


_10.4 Customize colors 10 GANTT DIAGRAM_

### 10.4 Customize colors

It also possible to customize colors.

@startgantt
[Prototype design] lasts 13 days
[Test prototype] lasts 4 days
[Test prototype] starts at [Prototype design]'s end
[Prototype design] is colored in Fuchsia/FireBrick
[Test prototype] is colored in GreenYellow/Green
@endgantt

### 10.5 Milestone

You can define Milestones using thehappensverb.

@startgantt
[Test prototype] lasts 10 days
[Prototype completed] happens at [Test prototype]'s end
[Setup assembly line] lasts 12 days
[Setup assembly line] starts at [Test prototype]'s end
@endgantt

### 10.6 Calendar

You can specify a starting date for the whole project. By default, the first task starts at this date.

@startgantt
Project starts the 20th of september 2017
[Prototype design] as [TASK1] lasts 13 days
[TASK1] is colored in Lavender/LightBlue
@endgantt

### 10.7 Close day

It is possible to close some day.

@startgantt
project starts the 2018/04/09
saturday are closed
sunday are closed
2018/05/01 is closed
2018/04/17 to 2018/04/19 is closed
[Prototype design] lasts 14 days
[Test prototype] lasts 4 days
[Test prototype] starts at [Prototype design]'s end
[Prototype design] is colored in Fuchsia/FireBrick
[Test prototype] is colored in GreenYellow/Green


_10.8 Simplified task succession 10 GANTT DIAGRAM_

@endgantt

### 10.8 Simplified task succession

It's possible to use thethenkeyword to denote consecutive tasks.

@startgantt
[Prototype design] lasts 14 days
then [Test prototype] lasts 4 days
then [Deploy prototype] lasts 6 days
@endgantt

You can also use arrow->

@startgantt
[Prototype design] lasts 14 days
[Build prototype] lasts 4 days
[Prepare test] lasts 6 days
[Prototype design] -> [Build prototype]
[Prototype design] -> [Prepare test]
@endgantt

### 10.9 Separator

You can use--to separate sets of tasks.

@startgantt
[Task1] lasts 10 days
then [Task2] lasts 4 days
-- Phase Two --
then [Task3] lasts 5 days
then [Task4] lasts 6 days
@endgantt

### 10.10 Working with resources

You can affect tasks on resources using theonkeyword and brackets for resource name.

@startgantt
[Task1] on {Alice} lasts 10 days
[Task2] on {Bob:50%} lasts 2 days


_10.11 Complex example 10 GANTT DIAGRAM_

then [Task3] on {Alice:25%} lasts 1 days
@endgantt

### 10.11 Complex example

It also possible to use theandconjunction.

You can also add delays in constraints.

@startgantt
[Prototype design] lasts 13 days and is colored in Lavender/LightBlue
[Test prototype] lasts 9 days and is colored in Coral/Green and starts 3 days after [Prototype design]'s end
[Write tests] lasts 5 days and ends at [Prototype design]'s end
[Hire tests writers] lasts 6 days and ends at [Write tests]'s start
[Init and write tests report] is colored in Coral/Green
[Init and write tests report] starts 1 day before [Test prototype]'s start and ends at [Test prototype]'s end
@endgantt


#### 11 MINDMAP

## 11 MindMap

MindMap diagram are still in beta: the syntax may change without notice.

### 11.1 OrgMode syntax

This syntax is compatible with OrgMode

@startmindmap
* Debian
** Ubuntu
*** Linux Mint
*** Kubuntu
*** Lubuntu
*** KDE Neon
** LMDE
** SolydXK
** SteamOS
** Raspbian with a very long name
*** <s>Raspmbc</s> => OSMC
*** <s>Raspyfi</s> => Volumio
@endmindmap

### 11.2 Removing box

You can remove the box drawing using an underscore.

@startmindmap
* root node
** some first level node
***_ second level node
***_ another second level node
***_ foo
***_ bar
***_ foobar
** another first level node


_11.3 Arithmetic notation 11 MINDMAP_

@endmindmap

### 11.3 Arithmetic notation

You can use the following notation to choose diagram side.

@startmindmap
+ OS
++ Ubuntu
+++ Linux Mint
+++ Kubuntu
+++ Lubuntu
+++ KDE Neon
++ LMDE
++ SolydXK
++ SteamOS
++ Raspbian
-- Windows 95
-- Windows 98
-- Windows NT
--- Windows 8
--- Windows 10
@endmindmap

### 11.4 Markdown syntax

This syntax is compatible with Markdown

@startmindmap


_11.5 Changing diagram direction 11 MINDMAP_

* root node
* some first level node
* second level node
* another second level node
* another first level node
@endmindmap

### 11.5 Changing diagram direction

It is possible to use both sides of the diagram.

@startmindmap
* count
** 100
*** 101
*** 102
** 200

left side

** A
*** AA
*** AB
** B
@endmindmap

### 11.6 Complete example

@startmindmap
caption figure 1
title My super title

* <&flag>Debian
** <&globe>Ubuntu
*** Linux Mint
*** Kubuntu
*** Lubuntu
*** KDE Neon
** <&graph>LMDE


_11.6 Complete example 11 MINDMAP_

** <&pulse>SolydXK
** <&people>SteamOS
** <&star>Raspbian with a very long name
*** <s>Raspmbc</s> => OSMC
*** <s>Raspyfi</s> => Volumio

header
My super header
endheader

center footer My super footer

legend right
Short
legend
endlegend
@endmindmap


#### 12 WORK BREAKDOWN STRUCTURE

## 12 Work Breakdown Structure

WBS diagram are still in beta: the syntax may change without notice.

### 12.1 OrgMode syntax

This syntax is compatible with OrgMode

@startwbs
* Business Process Modelling WBS
** Launch the project
*** Complete Stakeholder Research
*** Initial Implementation Plan
** Design phase
*** Model of AsIs Processes Completed
**** Model of AsIs Processes Completed1
**** Model of AsIs Processes Completed2
*** Measure AsIs performance metrics
*** Identify Quick Wins
** Complete innovate phase
@endwbs

### 12.2 Change direction

You can change direction using<and>

@startwbs
* Business Process Modelling WBS
** Launch the project
*** Complete Stakeholder Research
*** Initial Implementation Plan
** Design phase
*** Model of AsIs Processes Completed
****< Model of AsIs Processes Completed1
****> Model of AsIs Processes Completed2
***< Measure AsIs performance metrics
***< Identify Quick Wins


_12.3 Arithmetic notation 12 WORK BREAKDOWN STRUCTURE_

@endwbs

### 12.3 Arithmetic notation

You can use the following notation to choose diagram side.

@startwbs
+ New Job
++ Decide on Job Requirements
+++ Identity gaps
+++ Review JDs
++++ Sign-Up for courses
++++ Volunteer
++++ Reading
++- Checklist
+++- Responsibilities
+++- Location
++ CV Upload Done
+++ CV Updated
++++ Spelling & Grammar
++++ Check dates
---- Skills
+++ Recruitment sites chosen
@endwbs

You can use underscore_to remove box drawing.

@startwbs
+ Project


_12.3 Arithmetic notation 12 WORK BREAKDOWN STRUCTURE_

```
+ Part One
+ Task 1.1
```
- LeftTask 1.2
+ Task 1.3
+ Part Two
+ Task 2.1
+ Task 2.2
-_ Task 2.2.1 To the left boxless
-_ Task 2.2.2 To the Left boxless
+_ Task 2.2.3 To the right boxless
@endwbs


#### 13 MATHS

## 13 Maths

You can use AsciiMath or JLaTeXMath notation within PlantUML:

@startuml
:<math>int_0^1f(x)dx</math>;
:<math>x^2+y_1+z_12^34</math>;
note right
Try also
<math>d/dxf(x)=lim_(h->0)(f(x+h)-f(x))/h</math>
<latex>P(y|\mathbf{x}) \mbox{ or } f(\mathbf{x})+\epsilon</latex>
end note
@enduml

or:

@startuml
Bob -> Alice : Can you solve: <math>ax^2+bx+c=0</math>
Alice --> Bob: <math>x = (-b+-sqrt(b^2-4ac))/(2a)</math>
@enduml

### 13.1 Standalone diagram

You can also use@startmath/@endmathto create standalone AsciiMath formula.

@startmath
f(t)=(a_0)/2 + sum_(n=1)^ooa_ncos((npit)/L)+sum_(n=1)^oo b_n\ sin((npit)/L)
@endmath

Or use@startlatex/@endlatexto create standalone JLaTeXMath formula.

@startlatex
\sum_{i=0}^{n-1} (a_i + b_i^2)
@endlatex


_13.2 How is this working? 13 MATHS_

### 13.2 How is this working?

To draw those formulas, PlantUML uses two OpenSource projects:

- AsciiMath that converts AsciiMath notation to LaTeX expression.
- JLatexMath that displays mathematical formulas written in LaTeX. JLaTeXMath is the best Java library to
    display LaTeX code.

ASCIIMathTeXImg.js is small enough to be integrated into PlantUML standard distribution.

SinceJLatexMathisbigger, youhavetodownloaditseparately, thenunzipthe4jarfiles( _batik-all-1.7.jar_ , _jlatexmath-
minimal-1.0.3.jar_ , _jlm_cyrillic.jar_ and _jlm_greek.jar_ ) in the same folder as PlantUML.jar.


#### 14 COMMON COMMANDS

## 14 Common commands

### 14.1 Comments

Everything that starts withsimple quote 'is a comment.

You can also put comments on several lines using/'to start and'/to end.

### 14.2 Footer and header

You can use the commandsheaderorfooterto add a footer or a header on any generated diagram.

You can optionally specify if you want acenter,leftorrightfooter/header, by adding a keyword.

As for title, it is possible to define a header or a footer on several lines.

It is also possible to put some HTML into the header or footer.

@startuml
Alice -> Bob: Authentication Request

header
<font color=red>Warning:</font>
Do not use in production.
endheader

center footer Generated for demonstration

@enduml

### 14.3 Zoom

You can use thescalecommand to zoom the generated image.

You can use either a number or a fraction to define the scale factor. You can also specify either width or height (in
pixel). And you can also give both width and height : the image is scaled to fit inside the specified dimension.

- scale 1.5
- scale 2/3
- scale 200 width
- scale 200 height
- scale 200*100
- scale max 300*200
- scale max 1024 width
- scale max 800 height


_14.4 Title 14 COMMON COMMANDS_

@startuml
scale 180*90
Bob->Alice : hello
@enduml

### 14.4 Title

Thetitlekeywords is used to put a title. You can add newline using\nin the title description.

Some skinparam settings are available to put borders on the title.

@startuml
skinparam titleBorderRoundCorner 15
skinparam titleBorderThickness 2
skinparam titleBorderColor red
skinparam titleBackgroundColor Aqua-CadetBlue

title Simple communication\nexample

Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response

@enduml

You can use creole formatting in the title.

You can also define title on several lines usingtitleandend titlekeywords.

@startuml

title
<u>Simple</u> communication example
on <i>several</i> lines and using <back:cadetblue>creole tags</back>
end title

Alice -> Bob: Authentication Request
Bob -> Alice: Authentication Response

@enduml


_14.5 Caption 14 COMMON COMMANDS_

### 14.5 Caption

There is also acaptionkeyword to put a caption under the diagram.

@startuml

caption figure 1
Alice -> Bob: Hello

@enduml

### 14.6 Legend the diagram

Thelegendandend legendare keywords is used to put a legend.

You can optionally specify to haveleft,right,top,bottomorcenteralignment for the legend.

@startuml
Alice -> Bob : Hello
legend right
Short
legend
endlegend
@enduml

@startuml
Alice -> Bob : Hello
legend top left
Short


_14.6 Legend the diagram 14 COMMON COMMANDS_

legend
endlegend
@enduml


#### 15 SALT (WIREFRAME)

## 15 Salt (wireframe)

**Salt** is a subproject included in PlantUML that may help you to design graphical interface.

You can use either@startsaltkeyword, or@startumlfollowed by a line withsaltkeyword.

### 15.1 Basic widgets

A window must start and end with brackets. You can then define:

- Button using[and].
- Radio button using(and).
- Checkbox using[and].
- User text area using".

@startuml
salt
{
Just plain text
[This is my button]
() Unchecked radio
(X) Checked radio
[] Unchecked box
[X] Checked box
"Enter text here "
^This is a droplist^
}
@enduml

The goal of this tool is to discuss about simple and sample windows.

### 15.2 Using grid

A table is automatically created when you use an opening bracket{. And you have to use|to separate columns.

For example:

@startsalt
{
Login | "MyName "
Password | "**** "
[Cancel] | [ OK ]
}
@endsalt


_15.3 Group box 15 SALT (WIREFRAME)_

Just after the opening bracket, you can use a character to define if you want to draw lines or columns of the grid :

```
Symbol Result
# To display all vertical and horizontal lines
! To display all vertical lines
```
- To display all horizontal lines
+ To display external lines

@startsalt
{+
Login | "MyName "
Password | "**** "
[Cancel] | [ OK ]
}
@endsalt

### 15.3 Group box

more info

@startsalt
{^"My group box"
Login | "MyName "
Password | "**** "
[Cancel] | [ OK ]
}
@endsalt

### 15.4 Using separator

You can use several horizontal lines as separator.

@startsalt
{
Text1
..
"Some field"
==
Note on usage
~~
Another text
--
[Ok]
}
@endsalt


_15.5 Tree widget 15 SALT (WIREFRAME)_

### 15.5 Tree widget

To have a Tree, you have to start with{Tand to use+to denote hierarchy.

@startsalt
{
{T
+ World
++ America
+++ Canada
+++ USA
++++ New York
++++ Boston
+++ Mexico
++ Europe
+++ Italy
+++ Germany
++++ Berlin
++ Africa
}
}
@endsalt

### 15.6 Enclosing brackets

You can define subelements by opening a new opening bracket.

@startsalt
{
Name | " "
Modifiers: | { (X) public | () default | () private | () protected
[] abstract | [] final | [] static }
Superclass: | { "java.lang.Object " | [Browse...] }
}
@endsalt


_15.7 Adding tabs 15 SALT (WIREFRAME)_

### 15.7 Adding tabs

You can add tabs using{/notation. Note that you can use HTML code to have bold text.

@startsalt
{+
{/ <b>General | Fullscreen | Behavior | Saving }
{
{ Open image in: | ^Smart Mode^ }
[X] Smooth images when zoomed
[X] Confirm image deletion
[ ] Show hidden images
}
[Close]
}
@endsalt

Tab could also be vertically oriented:

@startsalt
{+
{/ <b>General
Fullscreen
Behavior
Saving } |
{
{ Open image in: | ^Smart Mode^ }
[X] Smooth images when zoomed
[X] Confirm image deletion
[ ] Show hidden images
[Close]
}
}
@endsalt

### 15.8 Using menu

You can add a menu by using{*notation.

@startsalt
{+
{* File | Edit | Source | Refactor }
{/ General | Fullscreen | Behavior | Saving }
{
{ Open image in: | ^Smart Mode^ }
[X] Smooth images when zoomed


_15.9 Advanced table 15 SALT (WIREFRAME)_

[X] Confirm image deletion
[ ] Show hidden images
}
[Close]
}
@endsalt

It is also possible to open a menu:

@startsalt
{+
{* File | Edit | Source | Refactor
Refactor | New | Open File | - | Close | Close All }
{/ General | Fullscreen | Behavior | Saving }
{
{ Open image in: | ^Smart Mode^ }
[X] Smooth images when zoomed
[X] Confirm image deletion
[ ] Show hidden images
}
[Close]
}
@endsalt

### 15.9 Advanced table

You can use two special notations for table :

- *to indicate that a cell with span with left
- .to denotate an empty cell

@startsalt
{#

. | Column 2 | Column 3
Row header 1 | value 1 | value 2
Row header 2 | A long cell | *
}
@endsalt


_15.10 OpenIconic 15 SALT (WIREFRAME)_

### 15.10 OpenIconic

OpenIconic is an very nice open source icon set. Those icons have been integrated into the creole parser, so you
can use them out-of-the-box. You can use the following syntax:<&ICON_NAME>.

@startsalt
{
Login<&person> | "MyName "
Password<&key> | "**** "
[Cancel <&circle-x>] | [OK <&account-login>]
}
@endsalt

The complete list is available on OpenIconic Website, or you can use the following special diagram:

@startuml
listopeniconic
@enduml

### 15.11 Include Salt

see: [http://forum.plantuml.net/2427/salt-with-minimum-flowchat-capabilities?show=2427#q2427](http://forum.plantuml.net/2427/salt-with-minimum-flowchat-capabilities?show=2427#q2427)

@startuml
(*) --> "
{{
salt
{+
<b>an example
choose one option
()one


_15.11 Include Salt 15 SALT (WIREFRAME)_

()two
[ok]
}
}}
" as choose

choose -right-> "
{{
salt
{+
<b>please wait
operation in progress
<&clock>
[cancel]
}
}}
" as wait
wait -right-> "
{{
salt
{+
<b>success
congratulations!
[ok]
}
}}
" as success

wait -down-> "
{{
salt
{+
<b>error
failed, sorry
[ok]
}
}}
"
@enduml

It can also be combined with define macro.


_15.11 Include Salt 15 SALT (WIREFRAME)_

@startuml
!unquoted function SALT($x)
"{{
salt
%invoke_void_func("_"+$x)
}}" as $x
!endfunction

!function _choose()
{+
<b>an example
choose one option
()one
()two
[ok]
}
!endfunction

!function _wait()
{+
<b>please wait
operation in progress
<&clock>
[cancel]
}
!endfunction

!function _success()
{+
<b>success
congratulations!
[ok]
}
!endfunction

!function _error()
{+
<b>error
failed, sorry
[ok]
}
!endfunction

(*) --> SALT(choose)
-right-> SALT(wait)
wait -right-> SALT(success)
wait -down-> SALT(error)
@enduml


_15.12 Scroll Bars 15 SALT (WIREFRAME)_

### 15.12 Scroll Bars

You can use "S" as scroll bar like in following examples:

@startsalt
{S
Message
.
.
.
.
}
@endsalt

@startsalt
{SI
Message
.
.
.
.
}
@endsalt

@startsalt
{S-
Message
.
.
.


_15.12 Scroll Bars 15 SALT (WIREFRAME)_

#### .

#### }

@endsalt


#### 16 CREOLE

## 16 Creole

A light Creole engine has been integrated into PlantUML to have a standardized way of defining text style.

All diagrams are now supporting this syntax.

Note that ascending compatibility with HTML syntax is preserved.

### 16.1 Emphasized text

@startuml
Alice -> Bob : hello --there--
... Some ~~long delay~~ ...
Bob -> Alice : ok
note left
This is **bold**
This is //italics//
This is ""monospaced""
This is --stroked--
This is __underlined__
This is ~~waved~~
end note
@enduml

### 16.2 List

@startuml
object demo {
* Bullet list
* Second item
}
note left
* Bullet list
* Second item
** Sub item
end note

legend
# Numbered list
# Second item
## Sub item
## Another sub item


_16.3 Escape character 16 CREOLE_

# Third item
end legend
@enduml

### 16.3 Escape character

You can use the tilde~to escape special creole characters.

@startuml
object demo {
This is not ~___underscored__.
This is not ~""monospaced"".
}
@enduml

### 16.4 Horizontal lines

@startuml
database DB1 as "
You can have horizontal line
----
Or double line
====
Or strong line
____
Or dotted line
..My title..
Enjoy!
"
note right
This is working also in notes
You can also add title in all these lines
==Title==
--Another title--
end note

@enduml


_16.5 Headings 16 CREOLE_

### 16.5 Headings

@startuml
usecase UC1 as "
= Extra-large heading
Some text
== Large heading
Other text
=== Medium heading
Information
....
==== Small heading"
@enduml

### 16.6 Legacy HTML

Some HTML tags are also working:

- <b>for bold text
- <u>or<u:#AAAAAA>or<u:colorName>for underline
- <i>for italic
- <s>or<s:#AAAAAA>or<s:colorName>for strike text
- <w>or<w:#AAAAAA>or<w:colorName>for wave underline text
- <color:#AAAAAA>or<color:colorName>
- <back:#AAAAAA>or<back:colorName>for background color
- <size:nn>to change font size
- <img:file>: the file must be accessible by the filesystem
- <img:http://plantuml.com/logo3.png>: the URL must be available from the Internet

@startuml
:* You can change <color:red>text color</color>
* You can change <back:cadetblue>background color</back>
* You can change <size:18>size</size>


_16.7 Table 16 CREOLE_

* You use <u>legacy</u> <b>HTML <i>tag</i></b>
* You use <u:red>color</u> <s:green>in HTML</s> <w:#0000FF>tag</w>
----
* Use image : <img:http://plantuml.com/logo3.png>
;
@enduml

### 16.7 Table

It is possible to build table.

@startuml
skinparam titleFontSize 14
title
Example of simple table
|= |= table |= header |
| a | table | row |
| b | table | row |
end title
[*] --> State1
@enduml

You can specify background colors for cells and lines.

@startuml
start
:Here is the result
|= |= table |= header |
| a | table | row |
|<#FF8080> red |<#80FF80> green |<#8080FF> blue |
<#yellow>| b | table | row |;
@enduml


_16.8 Tree 16 CREOLE_

### 16.8 Tree

You can use|_characters to build a tree.

@startuml
skinparam titleFontSize 14
title
Example of Tree
|_ First line
|_ **Bom(Model)**
|_ prop1
|_ prop2
|_ prop3
|_ Last line
end title
[*] --> State1
@enduml

### 16.9 Special characters

It's possible to use any unicode characters with&#syntax or<U+XXXX>

@startuml
usecase foo as "this is &#8734; long"
usecase bar as "this is also <U+221E> long"
@enduml

### 16.10 OpenIconic

OpenIconic is an very nice open source icon set. Those icons have been integrated into the creole parser, so you
can use them out-of-the-box.


_16.10 OpenIconic 16 CREOLE_

You can use the following syntax:<&ICON_NAME>.

@startuml
title: <size:20><&heart>Use of OpenIconic<&heart></size>
class Wifi
note left
Click on <&wifi>
end note
@enduml

The complete list is available on OpenIconic Website, or you can use the following special diagram:

@startuml
listopeniconic
@enduml


#### 17 DEFINING AND USING SPRITES

## 17 Defining and using sprites

A _Sprite_ is a small graphic element that can be used in diagrams.

In PlantUML, sprites are monochrome and can have either 4, 8 or 16 gray level.

To define a sprite, you have to use a hexadecimal digit between 0 and F per pixel.

Then you can use the sprite using<$XXX>where XXX is the name of the sprite.

@startuml
sprite $foo1 {
FFFFFFFFFFFFFFF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
FFFFFFFFFFFFFFF
}
Alice -> Bob : Testing <$foo1>
@enduml

You can scale the sprite.

@startuml
sprite $foo1 {
FFFFFFFFFFFFFFF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
F0123456789ABCF
FFFFFFFFFFFFFFF
}
Alice -> Bob : Testing <$foo1{scale=3}>
@enduml


_17.1 Encoding Sprite 17 DEFINING AND USING SPRITES_

### 17.1 Encoding Sprite

To encode sprite, you can use the command line like:

java -jar plantuml.jar -encodesprite 16z foo.png

wherefoo.pngis the image file you want to use (it will be converted to gray automatically).

After-encodesprite, you have to specify a format:4, 8, 16, 4z, 8zor16z.

The number indicates the gray level and the optionalzis used to enable compression in sprite definition.

### 17.2 Importing Sprite

You can also launch the GUI to generate a sprite from an existing image.

Click in the menubar then onFile/Open Sprite Window.

After copying an image into you clipboard, several possible definitions of the corresponding sprite will be displayed
: you will just have to pickup the one you want.

### 17.3 Examples

@startuml
sprite $printer [15x15/8z] NOtH3W0W208HxFz_kMAhj7lHWpa1XC716sz0Pq4MVPEWfBHIuxP3L6kbTcizR8tAhzaqFvXwvFfPEqm0
start
:click on <$printer> to print the page;
@enduml

@startuml
sprite $bug [15x15/16z] PKzR2i0m2BFMi15p__FEjQEqB1z27aeqCqixa8S4OT7C53cKpsHpaYPDJY_12MHM-BLRyywPhrrlw3qumqNThmXgd1TOterAZmOW8sgiJafogofWRwtV3nCF
sprite $printer [15x15/8z] NOtH3W0W208HxFz_kMAhj7lHWpa1XC716sz0Pq4MVPEWfBHIuxP3L6kbTcizR8tAhzaqFvXwvFfPEqm0
sprite $disk {
444445566677881
436000000009991
43600000000ACA1
53700000001A7A1
53700000012B8A1
53800000123B8A1
63800001233C9A1
634999AABBC99B1
744566778899AB1
7456AAAAA99AAB1
8566AFC228AABB1
8567AC8118BBBB1
867BD4433BBBBB1
39AAAAABBBBBBC1
}

```
title Use of sprites (<$printer>, <$bug>...)
```
```
class Example {
Can have some bug : <$bug>
Click on <$disk> to save
}
```

_17.3 Examples 17 DEFINING AND USING SPRITES_

```
note left : The printer <$printer> is available
```
@enduml


#### 18 SKINPARAM COMMAND

## 18 Skinparam command

You can change colors and font of the drawing using theskinparamcommand.

Example:

skinparam backgroundColor transparent

### 18.1 Usage

You can use this command :

- In the diagram definition, like any other commands,
- In an included file,
- In a configuration file, provided in the command line or the ANT task.

### 18.2 Nested

To avoid repetition, it is possible to nest definition. So the following definition :

skinparam xxxxParam1 value1
skinparam xxxxParam2 value2
skinparam xxxxParam3 value3
skinparam xxxxParam4 value4

is strictly equivalent to:

skinparam xxxx {
Param1 value1
Param2 value2
Param3 value3
Param4 value4
}

### 18.3 Black and White

You can force the use of a black&white output usingskinparam monochrome truecommand.

@startuml

skinparam monochrome true

actor User
participant "First Class" as A
participant "Second Class" as B
participant "Last Class" as C

User -> A: DoWork
activate A

A -> B: Create Request
activate B

B -> C: DoWork
activate C
C --> B: WorkDone
destroy C

B --> A: Request Created


_18.4 Shadowing 18 SKINPARAM COMMAND_

deactivate B

A --> User: Done
deactivate A

@enduml

### 18.4 Shadowing

You can disable the shadowing using theskinparam shadowing falsecommand.

@startuml

left to right direction

skinparam shadowing<<no_shadow>> false
skinparam shadowing<<with_shadow>> true

actor User
(Glowing use case) <<with_shadow>> as guc
(Flat use case) <<no_shadow>> as fuc
User -- guc
User -- fuc

@enduml


_18.5 Reverse colors 18 SKINPARAM COMMAND_

### 18.5 Reverse colors

You can force the use of a black&white output usingskinparam monochrome reversecommand. This can be
useful for black background environment.

@startuml

skinparam monochrome reverse

actor User
participant "First Class" as A
participant "Second Class" as B
participant "Last Class" as C

User -> A: DoWork
activate A

A -> B: Create Request
activate B

B -> C: DoWork
activate C
C --> B: WorkDone
destroy C

B --> A: Request Created
deactivate B

A --> User: Done
deactivate A

@enduml

### 18.6 Colors

You can use either standard color name or RGB code.


_18.7 Font color, name and size 18 SKINPARAM COMMAND_

transparentcan only be used for background of the image.

### 18.7 Font color, name and size

You can change the font for the drawing usingxxxFontColor,xxxFontSizeandxxxFontNameparameters.

Example:

skinparam classFontColor red
skinparam classFontSize 10
skinparam classFontName Aapex

You can also change the default font for all fonts usingskinparam defaultFontName.

Example:

skinparam defaultFontName Aapex

Please note the fontname is highly system dependent, so do not over use it, if you look for portability.Helvetica
andCouriershould be available on all system.

A lot of parameters are available. You can list them using the following command:

java -jar plantuml.jar -language

### 18.8 Text Alignment

Text alignment can be set up toleft,rightorcenter. You can also usedirectionorreverseDirection
values forsequenceMessageAlignwhich align text depending on arrow direction.

```
Param name Default value Comment
sequenceMessageAlign left Used for messages in sequence diagrams
sequenceReferenceAlign center Used forref overin sequence diagrams
```
@startuml
skinparam sequenceMessageAlign center
Alice -> Bob : Hi
Alice -> Bob : This is very long
@enduml


_18.9 Examples 18 SKINPARAM COMMAND_

### 18.9 Examples

@startuml
skinparam backgroundColor #EEEBDC
skinparam handwritten true

skinparam sequence {
ArrowColor DeepSkyBlue
ActorBorderColor DeepSkyBlue
LifeLineBorderColor blue
LifeLineBackgroundColor #A9DCDF

ParticipantBorderColor DeepSkyBlue
ParticipantBackgroundColor DodgerBlue
ParticipantFontName Impact
ParticipantFontSize 17
ParticipantFontColor #A9DCDF

ActorBackgroundColor aqua
ActorFontColor DeepSkyBlue
ActorFontSize 17
ActorFontName Aapex
}

actor User
participant "First Class" as A
participant "Second Class" as B
participant "Last Class" as C

User -> A: DoWork
activate A

A -> B: Create Request
activate B

B -> C: DoWork
activate C
C --> B: WorkDone
destroy C

B --> A: Request Created
deactivate B

A --> User: Done
deactivate A

@enduml


_18.9 Examples 18 SKINPARAM COMMAND_

@startuml
skinparam handwritten true

skinparam actor {
BorderColor black
FontName Courier
BackgroundColor<< Human >> Gold
}

skinparam usecase {
BackgroundColor DarkSeaGreen
BorderColor DarkSlateGray

BackgroundColor<< Main >> YellowGreen
BorderColor<< Main >> YellowGreen

ArrowColor Olive
}

User << Human >>
:Main Database: as MySql << Application >>
(Start) << One Shot >>
(Use the application) as (Use) << Main >>

User -> (Start)
User --> (Use)

MySql --> (Use)
@enduml


_18.9 Examples 18 SKINPARAM COMMAND_

@startuml
skinparam roundcorner 20
skinparam class {
BackgroundColor PaleGreen
ArrowColor SeaGreen
BorderColor SpringGreen
}
skinparam stereotypeCBackgroundColor YellowGreen

Class01 "1" *-- "many" Class02 : contains

Class03 o-- Class04 : aggregation
@enduml

@startuml

skinparam interface {
backgroundColor RosyBrown
borderColor orange
}

skinparam component {
FontSize 13
BackgroundColor<<Apache>> Red
BorderColor<<Apache>> #FF6655
FontName Courier
BorderColor black
BackgroundColor gold
ArrowFontName Impact
ArrowColor #FF6655
ArrowFontColor #777777
}

() "Data Access" as DA

DA - [First Component]
[First Component] ..> () HTTP : use


_18.10 List of all skinparam parameters 18 SKINPARAM COMMAND_

HTTP - [Web Server] << Apache >>
@enduml

@startuml
[AA] <<static lib>>
[BB] <<shared lib>>
[CC] <<static lib>>

node node1
node node2 <<shared node>>
database Production

skinparam component {
backgroundColor<<static lib>> DarkKhaki
backgroundColor<<shared lib>> Green
}

skinparam node {
borderColor Green
backgroundColor Yellow
backgroundColor<<shared node>> Magenta
}
skinparam databaseBackgroundColor Aqua
@enduml

### 18.10 List of all skinparam parameters

Since the documentation is not always up to date, you can have the complete list of parameters using this command:

java -jar plantuml.jar -language

Or you can generate a "diagram" with a list of all the skinparam parameters using:

@startuml
help skinparams
@enduml

That will give you the following result:


_18.10 List of all skinparam parameters 18 SKINPARAM COMMAND_


_18.10 List of all skinparam parameters 18 SKINPARAM COMMAND_

Youcanalsovieweachskinparamparameterswithitsresultsdisplayedathttps://plantuml-documentation.readthedocs.
io/en/latest/formatting/all-skin-params.html.


#### 19 PREPROCESSING

## 19 Preprocessing

Some minor preprocessing capabilities are included in **PlantUML** , and available for _all_ diagrams.

Those functionalities are very similar to the C language preprocessor, except that the special character#has been
changed to the exclamation mark!.

### 19.1 Migration notes

The actual preprocessor is an update from some legacy preprocessor.

Even if some legacy features are still supported with the actual preprocessor, you should not use them any more
(they might be removed in some long term future).

- You should not use!defineand!definelonganymore. Use!functionand variable definition instead.
    !defineshould be replaced by return function and!definelongshould be replaced by void function.
- !includenow allows multiple inclusions : you don't have to use!include_manyanymore
- !includenow accepts a URL, so you don't need!includeurl
- Some features (like%date%) have been replaced by builtin functions (for example%date())
- When calling a legacy!definelongmacro with no arguments, you do have to use parenthesis. You have
    to usemy_own_definelong()becausemy_own_definelongwithout parenthesis is not recognized by the
    new preprocessor.

Please contact us if you have any issues.

### 19.2 Variable definition

Although this is not mandatory, we highly suggest that variable names start with a$. There are two types of data:

- Integer number
- String - these must be surrounded by single quote or double quote.

Variables created outside function are **global** , that is you can access them from everywhere (including from func-
tions). You can emphasize this by using the optionalglobalkeyword when defining a variable.

@startuml
!$ab = "foo1"
!$cd = "foo2"
!global $ef = $ab + $cd

Alice -> Bob : $ab
Alice -> Bob : $cd
Alice -> Bob : $ef
@enduml


_19.3 Conditions 19 PREPROCESSING_

### 19.3 Conditions

- You can use expression in condition.
- _else_ is also implemented

@startuml
!$a = 10
!$ijk = "foo"
Alice -> Bob : A
!if ($ijk == "foo") && ($a+10>=4)
Alice -> Bob : yes
!else
Alice -> Bob : This should not appear
!endif
Alice -> Bob : B
@enduml

### 19.4 Void function

- Function names _must_ start with a$
- Argument names _must_ start with a$
- Void functions can call other void functions

Example:

@startuml
!function msg($source, $destination)
$source --> $destination
!endfunction

!function init_class($name)
class $name {
$addCommonMethod()
}
!endfunction

!function $addCommonMethod()
toString()
hashCode()
!endfunction

init_class("foo1")
init_class("foo2")
msg("foo1", "foo2")
@enduml


_19.5 Return function 19 PREPROCESSING_

Variables defined in functions are **local**. It means that the variable is destroyed when the function ends.

### 19.5 Return function

A return function does not output any text. It just define a function that you can call:

- directly in variable definition or in diagram text
- from other return function
- from other void function
- Function name _should_ start by a$
- Argument names _should_ start by a$

@startuml
!function $double($a)
!return $a + $a
!endfunction

Alice -> Bob : The double of 3 is $double(3)
@enduml

It is possible to shorten simple function definition in one line:

@startuml
!function $double($a) return $a + $a

Alice -> Bob : The double of 3 is $double(3)
Alice -> Bob : $double("This work also for strings.")
@enduml


_19.6 Default argument value 19 PREPROCESSING_

As in void function, variable are local by default (they are destroyed when the function is exited). However, you
can access to global variables from function. However, you can use thelocalkeyword to create a local variable
if ever a global variable exists with the same name.

@startuml
!function $dummy()
!local $ijk = "local"
Alice -> Bob : $ijk
!endfunction

!global $ijk = "foo"

Alice -> Bob : $ijk
$dummy()
Alice -> Bob : $ijk
@enduml

### 19.6 Default argument value

In both return and void functions, you can define default values for arguments.

@startuml
!function $inc($value, $step=1)
!return $value + $step
!endfunction

Alice -> Bob : Just one more $inc(3)
Alice -> Bob : Add two to three : $inc(3, 2)
@enduml

Only arguments at the end of the parameter list can have default values.

@startuml
!function defaulttest($x, $y="DefaultY", $z="DefaultZ")
note over Alice
x = $x
y = $y
z = $z
end note
!endfunction


_19.7 Unquoted function 19 PREPROCESSING_

defaulttest(1, 2, 3)
defaulttest(1, 2)
defaulttest(1)
@enduml

### 19.7 Unquoted function

By default, you have to put quotes when you call a function. It is possible to use theunquotedkeyword to indicate
that a function does not require quotes for its arguments.

@startuml
!unquoted function id($text1, $text2="FOO") return $text1 + $text2

alice -> bob : id(aa)
alice -> bob : id(ab,cd)
@enduml

### 19.8 Including files or URL

Use the!includedirective to include file in your diagram. Using URL, you can also include file from Internet/In-
tranet.

Imagine you have the very same class that appears in many diagrams. Instead of duplicating the description of this
class, you can define a file that contains the description.

@startuml

!include List.iuml
List <|.. ArrayList
@enduml


_19.9 Including Subpart 19 PREPROCESSING_

**File List.iuml**

interface List
List : int size()
List : void clear()

The fileList.iumlcan be included in many diagrams, and any modification in this file will change all diagrams
that include it.

You can also put several@startuml/@endumltext block in an included file and then specify which block you
want to include adding!0where 0 is the block number. The!0notation denotes the first diagram.

For example, if you use!include foo.txt!1, the second@startuml/@endumlblock withinfoo.txtwill be
included.

Youcanalsoputanidtosome@startuml/@endumltextblockinanincludedfileusing@startuml(id=MY_OWN_ID)
syntax and then include the block adding!MY_OWN_IDwhen including the file, so using something like!include
foo.txt!MY_OWN_ID.

By default, a file can only be included once. You can use!include_manyinstead of!includeif you want to
include some file several times. Note that there is also a!include_oncedirective that raises an error if a file is
included several times.

### 19.9 Including Subpart

You can also use!startsub NAMEand!endsubto indicate sections of text to include from other files using
!includesub. For example:

**file1.puml:**

@startuml

A -> A : stuff1
!startsub BASIC
B -> B : stuff2
!endsub
C -> C : stuff3
!startsub BASIC
D -> D : stuff4
!endsub
@enduml

file1.puml would be rendered exactly as if it were:

@startuml

A -> A : stuff1
B -> B : stuff2
C -> C : stuff3
D -> D : stuff4
@enduml


_19.10 Builtin functions 19 PREPROCESSING_

However, this would also allow you to have another file2.puml like this:

**file2.puml**

@startuml

title this contains only B and D
!includesub file1.puml!BASIC
@enduml

This file would be rendered exactly as if:

@startuml

title this contains only B and D
B -> B : stuff2
D -> D : stuff4
@enduml

### 19.10 Builtin functions

Some functions are defined by default. Their name starts by%

```
Name Description Example Return
%strlen Calculate the length of a String %strlen("foo") 3 in the example
%substr Extract a substring. Takes 2 or 3 arguments|%substr("abcdef", 3, 2) "de"in the example
%strpos Search a substring in a string %strpos("abcdef", "ef") 4 (position ofef)
%intval Convert a String to Int %intval("42") 42
%file_exists Check if a file exists on the local filesystem %file_exists("c:/foo/dummy.txt") trueif the file exists
%function_exists Check if a function exists %function_exists("$some_function") trueif the function has been defined
%variable_exists Check if a variable exists %variable_exists("$my_variable") trueif the variable has been defined exists
%set_variable_value Set a global variable %set_variable_value("$my_variable", "some_value") An empty string
%get_variable_value Retrieve some variable value %get_variable_value("$my_variable") the value of the variable
%getenv Retrieve environment variable value %getenv("OS") The value ofOSvariable
%dirpath Retrieve current dirpath %dirpath() Current path
%filename Retrieve current filename %filename() Current filename
%date Retrieve current date. You can provide an optional format for the date %date("yyyy.MM.dd at HH:mm") Current date
%true Return alwaystrue %true() true
%false Return alwaysfalse %false() false
%not Return the logical negation of an expression %not(2+2==4) falsein that example
```
### 19.11 Logging

You can use!logto add some log output when generating the diagram. This has no impact at all on the diagram
itself. However, those logs are printed in the command line's output stream. This could be useful for debug purpose.

@startuml
!function bold($text)
!$result = "<b>"+ $text +"</b>"
!log Calling bold function with $text. The result is $result
!return $result
!endfunction

Alice -> Bob : This is bold("bold")
Alice -> Bob : This is bold("a second call")
@enduml


_19.12 Memory dump 19 PREPROCESSING_

### 19.12 Memory dump

You can use!memory_dumpto dump the full content of the memory when generating the diagram. An optional
string can be put after!memory_dump. This has no impact at all on the diagram itself. This could be useful for
debug purpose.

@startuml
!function $inc($string)
!$val = %intval($string)
!log value is $val
!dump_memory
!return $val+1
!endfunction

Alice -> Bob : 4 $inc("3")
!unused = "foo"
!dump_memory EOF
@enduml

### 19.13 Assertion

You can put assertion in your diagram.

@startuml
Alice -> Bob : Hello
!assert %strpos("abcdef", "cd")==3 : "This always fail"
@enduml


_19.14 Building custom library 19 PREPROCESSING_

### 19.14 Building custom library

It's possible to package a set of included files into a single .zip or .jar archive. This single zip/jar can then be
imported into your diagram using!importdirective.

Once the library has been imported, you can!includefile from this single zip/jar.

**Example:**

@startuml

!import /path/to/customLibrary.zip
' This just adds "customLibrary.zip" in the search path

!include myFolder/myFile.iuml
' Assuming that myFolder/myFile.iuml is located somewhere
' either inside "customLibrary.zip" or on the local filesystem

...

### 19.15 Search path

You can specify the java propertyplantuml.include.pathin the command line.

For example:

java -Dplantuml.include.path="c:/mydir" -jar plantuml.jar atest1.txt

Note the this -D option has to put before the -jar option. -D options after the -jar option will be used to define
constants within plantuml preprocessor.

### 19.16 Argument concatenation

It is possible to append text to a macro argument using the##syntax.

@startuml
!unquoted function COMP_TEXTGENCOMP(name)
[name] << Comp >>
interface Ifc << IfcType >> AS name##Ifc
name##Ifc - [name]
!endfunction


_19.17 Dynamic function invocation 19 PREPROCESSING_

COMP_TEXTGENCOMP(dummy)
@enduml

### 19.17 Dynamic function invocation

You can dynamically invoke a void function using the special%invoke_void_func()void function. This function
takes as first argument the name of the actual void function to be called. The following argument are copied to the
called function.

For example, you can have:

@startuml
!function $go()
Bob -> Alice : hello
!endfunction

!$wrapper = "$go"

%invoke_void_func($wrapper)
@enduml

For return functions, you can use the corresponding special function%call_user_func():

@startuml
!function bold($text)
!return "<b>"+ $text +"</b>"
!endfunction

Alice -> Bob : %call_user_func("bold", "Hello") there
@enduml


#### 20 UNICODE

## 20 Unicode

The PlantUML language use _letters_ to define actor, usecase and soon.

But _letters_ are not only A-Z latin characters, it could be _any kind of letter from any language_.

### 20.1 Examples

@startuml
skinparam handwritten true
skinparam backgroundColor #EEEBDC

actor 使用者
participant "頭等艙" as A
participant "第二類" as B
participant "最後一堂課" as 別的東西

使用者-> A: 完成這項工作
activate A

A -> B:創建請求
activate B

B ->別的東西: 創建請求
activate別的東西
別的東西 --> B: 這項工作完成
destroy別的東西

B --> A:請求創建
deactivate B

A -->使用者:做完
deactivate A
@enduml

@startuml

(*) --> "膩平台"
--> === S1 ===


_20.1 Examples 20 UNICODE_

#### -->鞠躬向公眾

#### --> === S2 ===

#### -->這傢伙波武器

#### --> (*)

skinparam backgroundColor #AAFFFF
skinparam activityStartColor red
skinparam activityBarColor SaddleBrown
skinparam activityEndColor Silver
skinparam activityBackgroundColor Peru
skinparam activityBorderColor Peru
@enduml

@startuml

skinparam usecaseBackgroundColor DarkSeaGreen
skinparam usecaseArrowColor Olive
skinparam actorBorderColor black
skinparam usecaseBorderColor DarkSlateGray

使用者<< 人類 >>
"主數據庫" as數據庫 << 應用程式>>
(草創) <<一桿 >>
"主数据燕" as (贏余) << 基本的>>

使用者-> (草創)
使用者--> (贏余)

數據庫 --> (贏余)
@enduml


_20.2 Charset 20 UNICODE_

@startuml

() "Σωκράτηςψεύτης" as Σωκράτης

Σωκράτης - [Πτηνά πολεμοχαρής]

[Πτηνά πολεμοχαρής] ..> () Αθήνα : Αυτές οι φράσειςσημαίνουν τίποτα

@enduml

### 20.2 Charset

The default charset used when _reading_ the text files containing the UML text description is system dependent.

Normally, it should just be fine, but in some case, you may want to the use another charset. For example, with the
command line:

java -jar plantuml.jar -charset UTF-8 files.txt

Or, with the ant task:

<!-- Put images in c:/images directory -->
<target name="main">
<plantuml dir="./src" charset="UTF-8" />

Depending of your Java installation, the following charset should be available:ISO-8859-1,UTF-8,UTF-16BE,
UTF-16LE,UTF-16.


#### 21 STANDARD LIBRARY

## 21 Standard Library

This page explains the official Standard Library for PlantUML This Standard Library is now included in official
releases of PlantUML. Including files follows the C convention for "C standard library" (see https://en.wikipedia.
org/wiki/C_standard_library )

Contents of the library come from third party contributors. We thank them for their usefull contribution!

### 21.1 AWS library

https://github.com/milo-minderbinder/AWS-PlantUML

The AWS library consists of Amazon AWS icons, it provides icons of two different sizes.

Use it by including the file that contains the sprite, eg:!include <aws/Storage/AmazonS3/AmazonS3>. When
imported, you can use the sprite as normally you would, using<$sprite_name>.

You may also include thecommon.pumlfile, eg:!include <aws/common>, which contains helper macros de-
fined. With thecommon.pumlimported, you can use theNAME_OF_SPRITE(parameters...)macro.

Example of usage:

@startuml
!include <aws/common>
!include <aws/Storage/AmazonS3/AmazonS3>
!include <aws/Storage/AmazonS3/bucket/bucket>

AMAZONS3(s3_internal)
AMAZONS3(s3_partner,"Vendor's S3")
s3_internal <- s3_partner
@enduml

### 21.2 Azure library

https://github.com/RicardoNiepel/Azure-PlantUML/

The Azure library consists of Microsoft Azure icons.

Use it by including the file that contains the sprite, eg:!include <azure/Analytics/AzureEventHub.puml>.
When imported, you can use the sprite as normally you would, using<$sprite_name>.

You may also include theAzureCommon.pumlfile, eg:!include <azure/AzureCommon.puml>, which contains
helpermacrosdefined. WiththeAzureCommon.pumlimported, youcanusetheNAME_OF_SPRITE(parameters...)
macro.

Example of usage:

@startuml
!include <azure/AzureCommon.puml>
!include <azure/Analytics/AzureEventHub.puml>
!include <azure/Analytics/AzureStreamAnalytics.puml>
!include <azure/Databases/AzureCosmosDb.puml>

left to right direction


_21.3 Cloud Insight 21 STANDARD LIBRARY_

agent "Device Simulator" as devices #fff

AzureEventHub(fareDataEventHub, "Fare Data", "PK: Medallion HackLicense VendorId; 3 TUs")
AzureEventHub(tripDataEventHub, "Trip Data", "PK: Medallion HackLicense VendorId; 3 TUs")
AzureStreamAnalytics(streamAnalytics, "Stream Processing", "6 SUs")
AzureCosmosDb(outputCosmosDb, "Output Database", "1,000 RUs")

devices --> fareDataEventHub
devices --> tripDataEventHub
fareDataEventHub --> streamAnalytics
tripDataEventHub --> streamAnalytics
streamAnalytics --> outputCosmosDb
@enduml

### 21.3 Cloud Insight

https://github.com/rabelenda/cicon-plantuml-sprites

This repository contains PlantUML sprites generated from Cloudinsight icons, which can easily be used in Plan-
tUML diagrams for nice visual representation of popular technologies.

@startuml
!include <cloudinsight/tomcat>
!include <cloudinsight/kafka>
!include <cloudinsight/java>
!include <cloudinsight/cassandra>

title Cloudinsight sprites example

skinparam monochrome true

rectangle "<$tomcat>\nwebapp" as webapp
queue "<$kafka>" as kafka
rectangle "<$java>\ndaemon" as daemon
database "<$cassandra>" as cassandra

webapp -> kafka
kafka -> daemon
daemon --> cassandra


_21.4 Devicons and Font Awesome library 21 STANDARD LIBRARY_

@enduml

### 21.4 Devicons and Font Awesome library

https://github.com/tupadr3/plantuml-icon-font-sprites

These two library consists respectively of Devicons and Font Awesome libraries of icons.

Use it by including the file that contains the sprite, eg:!include <font-awesome/align_center>. When
imported, you can use the sprite as normally you would, using<$sprite_name>.

You may also include thecommon.pumlfile, eg:!include <font-awesome/common>, which contains helper
macros defined. With thecommon.pumlimported, you can use theNAME_OF_SPRITE(parameters...)macro.

Example of usage:

@startuml
!include <tupadr3/common>
!include <tupadr3/font-awesome/server>
!include <tupadr3/font-awesome/database>

title Styling example

FA_SERVER(web1,web1) #Green
FA_SERVER(web2,web2) #Yellow
FA_SERVER(web3,web3) #Blue
FA_SERVER(web4,web4) #YellowGreen

FA_DATABASE(db1,LIVE,database,white) #RoyalBlue
FA_DATABASE(db2,SPARE,database) #Red

db1 <--> db2

web1 <--> db1
web2 <--> db1
web3 <--> db1
web4 <--> db1
@enduml


_21.5 Google Material Icons 21 STANDARD LIBRARY_

@startuml
!include <tupadr3/common>
!include <tupadr3/devicons/mysql>

DEV_MYSQL(db1)
DEV_MYSQL(db2,label of db2)
DEV_MYSQL(db3,label of db3,database)
DEV_MYSQL(db4,label of db4,database,red) #DeepSkyBlue
@enduml

### 21.5 Google Material Icons

https://github.com/Templarian/MaterialDesign

This library consists of a free Material style icons from Google and other artists.

Use it by including the file that contains the sprite, eg:!include <material/ma_folder_move>. When im-
ported, you can use the sprite as normally you would, using<$ma_sprite_name>. Notice that this library requires
anma_prefix on sprites names, this is to avoid clash of names if multiple sprites have the same name on different
libraries.

You may also include thecommon.pumlfile, eg:!include <material/common>, which contains helper macros
defined. With thecommon.pumlimported, you can use theMA_NAME_OF_SPRITE(parameters...)macro, note


_21.6 Office 21 STANDARD LIBRARY_

again the use of the prefixMA_.

Example of usage:

@startuml
!include <material/common>
' To import the sprite file you DON'T need to place a prefix!
!include <material/folder_move>

MA_FOLDER_MOVE(Red, 1, dir, rectangle, "A label")
@enduml

Notes

When mixing sprites macros with other elements you may get a syntax error if, for example, trying to add a rectangle
along with classes. In those cases, add{and}after the macro to create the empty rectangle.

Example of usage:

@startuml
!include <material/common>
' To import the sprite file you DON'T need to place a prefix!
!include <material/folder_move>

MA_FOLDER_MOVE(Red, 1, dir, rectangle, "A label") {
}

class foo {
bar
}
@enduml

### 21.6 Office

https://github.com/Roemer/plantuml-office

There are sprites (*.puml) and colored png icons available. Be aware that the sprites are all only monochrome even
if they have a color in their name (due to automatically generating the files). You can either color the sprites with
the macro (see examples below) or directly use the fully colored pngs. See the following examples on how to use
the sprites, the pngs and the macros.

Example of usage:

@startuml
!include <tupadr3/common>

!include <office/Servers/database_server>
!include <office/Servers/application_server>
!include <office/Concepts/firewall_orange>
!include <office/Clouds/cloud_disaster_red>


_21.6 Office 21 STANDARD LIBRARY_

title Office Icons Example

package "Sprites" {
OFF_DATABASE_SERVER(db,DB)
OFF_APPLICATION_SERVER(app,App-Server)
OFF_FIREWALL_ORANGE(fw,Firewall)
OFF_CLOUD_DISASTER_RED(cloud,Cloud)
db <-> app
app <--> fw
fw <.left.> cloud
}

@enduml

@startuml
!include <tupadr3/common>

!include <office/servers/database_server>
!include <office/servers/application_server>
!include <office/Concepts/firewall_orange>
!include <office/Clouds/cloud_disaster_red>

' Used to center the label under the images
skinparam defaultTextAlignment center

title Extended Office Icons Example

package "Use sprite directly" {
[Some <$cloud_disaster_red> object]
}

package "Different macro usages" {
OFF_CLOUD_DISASTER_RED(cloud1)
OFF_CLOUD_DISASTER_RED(cloud2,Default with text)
OFF_CLOUD_DISASTER_RED(cloud3,Other shape,Folder)
OFF_CLOUD_DISASTER_RED(cloud4,Even another shape,Database)
OFF_CLOUD_DISASTER_RED(cloud5,Colored,Rectangle, red)
OFF_CLOUD_DISASTER_RED(cloud6,Colored background) #red
}
@enduml


_21.7 ArchiMate 21 STANDARD LIBRARY_

### 21.7 ArchiMate

https://github.com/ebbypeter/Archimate-PlantUML

This repository contains ArchiMate PlantUML macros and other includes for creating Archimate Diagrams easily
and consistantly.

@startuml
!includeurl https://raw.githubusercontent.com/ebbypeter/Archimate-PlantUML/master/Archimate.puml

title Archimate Sample - Internet Browser

' Elements
Business_Object(businessObject, "A Business Object")
Business_Process(someBusinessProcess,"Some Business Process")
Business_Service(itSupportService, "IT Support for Business (Application Service)")

Application_DataObject(dataObject, "Web Page Data \n 'on the fly'")
Application_Function(webpageBehaviour, "Web page behaviour")
Application_Component(ActivePartWebPage, "Active Part of the web page \n 'on the fly'")

Technology_Artifact(inMemoryItem,"in memory / 'on the fly' html/javascript")
Technology_Service(internetBrowser, "Internet Browser Generic & Plugin")
Technology_Service(internetBrowserPlugin, "Some Internet Browser Plugin")
Technology_Service(webServer, "Some web server")

'Relationships
Rel_Flow_Left(someBusinessProcess, businessObject, "")
Rel_Serving_Up(itSupportService, someBusinessProcess, "")
Rel_Specialization_Up(webpageBehaviour, itSupportService, "")
Rel_Flow_Right(dataObject, webpageBehaviour, "")
Rel_Specialization_Up(dataObject, businessObject, "")
Rel_Assignment_Left(ActivePartWebPage, webpageBehaviour, "")
Rel_Specialization_Up(inMemoryItem, dataObject, "")
Rel_Realization_Up(inMemoryItem, ActivePartWebPage, "")
Rel_Specialization_Right(inMemoryItem,internetBrowser, "")
Rel_Serving_Up(internetBrowser, webpageBehaviour, "")
Rel_Serving_Up(internetBrowserPlugin, webpageBehaviour, "")
Rel_Aggregation_Right(internetBrowser, internetBrowserPlugin, "")
Rel_Access_Up(webServer, inMemoryItem, "")


_21.8 Miscellaneous 21 STANDARD LIBRARY_

Rel_Serving_Up(webServer, internetBrowser, "")
@enduml

### 21.8 Miscellaneous

You can list standard library folders using the special diagram:

@startuml
stdlib
@enduml


_21.8 Miscellaneous 21 STANDARD LIBRARY_

It is also possible to use the command linejava -jar plantuml.jar -stdlibto display the same list.

Finally, you can extract the full standard library sources usingjava -jar plantuml.jar -extractstdlib.
All files will be extracted in the folderstdlib.

Sources used to build official PlantUML releases are hosted here https://github.com/plantuml/plantuml-stdlib.You
can create Pull Request to update or add some library if you find it relevant.


#### CONTENTS CONTENTS

## Contents

**1 Sequence Diagram 1**
1.1 Basic examples............................................ 1
1.2 Declaring participant......................................... 1
1.3 Use non-letters in participants.................................... 3
1.4 Message to Self............................................ 3
1.5 Change arrow style.......................................... 3
1.6 Change arrow color.......................................... 4
1.7 Message sequence numbering.................................... 4
1.8 Page Title, Header and Footer.................................... 6
1.9 Splitting diagrams........................................... 7
1.10 Grouping message.......................................... 8
1.11 Notes on messages.......................................... 9
1.12 Some other notes........................................... 10
1.13 Changing notes shape......................................... 10
1.14 Creole and HTML........................................... 11
1.15 Divider................................................ 12
1.16 Reference............................................... 13
1.17 Delay................................................. 13
1.18 Space................................................. 14
1.19 Lifeline Activation and Destruction................................. 15
1.20 Return................................................. 16
1.21 Participant creation.......................................... 17
1.22 Shortcut syntax for activation, deactivation, creation........................ 17
1.23 Incoming and outgoing messages................................... 18
1.24 Anchors and Duration......................................... 19
1.25 Stereotypes and Spots......................................... 20
1.26 More information on titles...................................... 21
1.27 Participants encompass........................................ 22
1.28 Removing Foot Boxes........................................ 23
1.29 Skinparam............................................... 23
1.30 Changing padding........................................... 25

**2 Use Case Diagram 27**
2.1 Usecases................................................ 27
2.2 Actors................................................. 27
2.3 Usecases description......................................... 28
2.4 Basic example............................................. 28
2.5 Extension............................................... 29
2.6 Using notes.............................................. 29
2.7 Stereotypes.............................................. 30
2.8 Changing arrows direction...................................... 31
2.9 Splitting diagrams........................................... 32
2.10 Left to right direction......................................... 32
2.11 Skinparam............................................... 33
2.12 Complete example.......................................... 34

**3 Class Diagram 35**
3.1 Relations between classes....................................... 35
3.2 Label on relations........................................... 36
3.3 Adding methods............................................ 37
3.4 Defining visibility........................................... 38
3.5 Abstract and Static.......................................... 38
3.6 Advanced class body......................................... 39
3.7 Notes and stereotypes......................................... 39
3.8 More on notes............................................. 40
3.9 Note on links............................................. 41
3.10 Abstract class and interface...................................... 42


#### CONTENTS CONTENTS

```
3.11 Using non-letters........................................... 43
3.12 Hide attributes, methods......................................... 43
3.13 Hide classes.............................................. 44
3.14 Use generics.............................................. 45
3.15 Specific Spot............................................. 45
3.16 Packages............................................... 45
3.17 Packages style............................................. 46
3.18 Namespaces.............................................. 47
3.19 Automatic namespace creation.................................... 48
3.20 Lollipop interface........................................... 49
3.21 Changing arrows direction...................................... 49
3.22 Association classes.......................................... 50
3.23 Skinparam............................................... 51
3.24 Skinned Stereotypes.......................................... 51
3.25 Color gradient............................................. 52
3.26 Help on layout............................................. 53
3.27 Splitting large files.......................................... 53
```
**4 Activity Diagram 55**
4.1 Simple Activity............................................ 55
4.2 Label on arrows............................................ 55
4.3 Changing arrow direction....................................... 55
4.4 Branches............................................... 56
4.5 More on Branches........................................... 57
4.6 Synchronization............................................ 58
4.7 Long activity description....................................... 59
4.8 Notes................................................. 59
4.9 Partition................................................ 60
4.10 Skinparam............................................... 61
4.11 Octagon................................................ 62
4.12 Complete example.......................................... 62

**5 Activity Diagram (beta) 65**
5.1 Simple Activity............................................ 65
5.2 Start/Stop............................................... 65
5.3 Conditional.............................................. 66
5.4 Repeat loop.............................................. 67
5.5 While loop.............................................. 68
5.6 Parallel processing.......................................... 68
5.7 Notes................................................. 69
5.8 Colors................................................. 70
5.9 Arrows................................................ 70
5.10 Connector............................................... 71
5.11 Grouping............................................... 71
5.12 Swimlanes............................................... 72
5.13 Detach................................................. 73
5.14 SDL.................................................. 74
5.15 Complete example.......................................... 75

**6 Component Diagram 77**
6.1 Components.............................................. 77
6.2 Interfaces............................................... 77
6.3 Basic example............................................. 78
6.4 Using notes.............................................. 78
6.5 Grouping Components........................................ 78
6.6 Changing arrows direction...................................... 80
6.7 Use UML2 notation.......................................... 81
6.8 Long description........................................... 82
6.9 Individual colors........................................... 82


#### CONTENTS CONTENTS

```
6.10 Using Sprite in Stereotype...................................... 82
6.11 Skinparam............................................... 83
```
**7 State Diagram 85**
7.1 Simple State.............................................. 85
7.2 Change state rendering........................................ 85
7.3 Composite state............................................ 86
7.4 Long name.............................................. 87
7.5 Fork.................................................. 88
7.6 Concurrent state............................................ 89
7.7 Arrow direction............................................ 90
7.8 Note.................................................. 91
7.9 More in notes............................................. 92
7.10 Skinparam............................................... 92

**8 Object Diagram 94**
8.1 Definition of objects......................................... 94
8.2 Relations between objects....................................... 94
8.3 Adding fields............................................. 94
8.4 Common features with class diagrams................................ 95

**9 Timing Diagram 96**
9.1 Declaring participant......................................... 96
9.2 Adding message............................................ 96
9.3 Relative time............................................. 97
9.4 Participant oriented.......................................... 98
9.5 Setting scale.............................................. 98
9.6 Initial state.............................................. 98
9.7 Intricated state............................................. 99
9.8 Hidden state.............................................. 100
9.9 Adding constraint........................................... 100
9.10 Adding texts.............................................. 101

**10 Gantt Diagram 102**
10.1 Declaring tasks............................................ 102
10.2 Adding constraints.......................................... 102
10.3 Short names.............................................. 102
10.4 Customize colors........................................... 103
10.5 Milestone............................................... 103
10.6 Calendar................................................ 103
10.7 Close day............................................... 103
10.8 Simplified task succession...................................... 104
10.9 Separator............................................... 104
10.10Working with resources........................................ 104
10.11Complex example........................................... 105

**11 MindMap 106**
11.1 OrgMode syntax........................................... 106
11.2 Removing box............................................. 106
11.3 Arithmetic notation.......................................... 107
11.4 Markdown syntax........................................... 107
11.5 Changing diagram direction..................................... 108
11.6 Complete example.......................................... 108

**12 Work Breakdown Structure 110**
12.1 OrgMode syntax........................................... 110
12.2 Change direction........................................... 110
12.3 Arithmetic notation.......................................... 111


#### CONTENTS CONTENTS

**13 Maths 113**
13.1 Standalone diagram.......................................... 113
13.2 How is this working ?......................................... 114

**14 Common commands 115**
14.1 Comments............................................... 115
14.2 Footer and header........................................... 115
14.3 Zoom................................................. 115
14.4 Title.................................................. 116
14.5 Caption................................................ 117
14.6 Legend the diagram.......................................... 117

**15 Salt (wireframe) 119**
15.1 Basic widgets............................................. 119
15.2 Using grid............................................... 119
15.3 Group box............................................... 120
15.4 Using separator............................................ 120
15.5 Tree widget.............................................. 121
15.6 Enclosing brackets.......................................... 121
15.7 Adding tabs.............................................. 122
15.8 Using menu.............................................. 122
15.9 Advanced table............................................ 123
15.10OpenIconic.............................................. 124
15.11Include Salt.............................................. 124
15.12Scroll Bars.............................................. 127

**16 Creole 129**
16.1 Emphasized text............................................ 129
16.2 List.................................................. 129
16.3 Escape character........................................... 130
16.4 Horizontal lines............................................ 130
16.5 Headings............................................... 131
16.6 Legacy HTML............................................ 131
16.7 Table................................................. 132
16.8 Tree.................................................. 133
16.9 Special characters........................................... 133
16.10OpenIconic.............................................. 133

**17 Defining and using sprites 135**
17.1 Encoding Sprite............................................ 136
17.2 Importing Sprite............................................ 136
17.3 Examples............................................... 136

**18 Skinparam command 138**
18.1 Usage................................................. 138
18.2 Nested................................................. 138
18.3 Black and White........................................... 138
18.4 Shadowing.............................................. 139
18.5 Reverse colors............................................. 140
18.6 Colors................................................. 140
18.7 Font color, name and size....................................... 141
18.8 Text Alignment............................................ 141
18.9 Examples............................................... 142
18.10List of all skinparam parameters................................... 145

**19 Preprocessing 148**
19.1 Migration notes............................................ 148
19.2 Variable definition.......................................... 148
19.3 Conditions............................................... 149


#### CONTENTS CONTENTS

```
19.4 Void function............................................. 149
19.5 Return function............................................ 150
19.6 Default argument value........................................ 151
19.7 Unquoted function.......................................... 152
19.8 Including files or URL........................................ 152
19.9 Including Subpart........................................... 153
19.10Builtin functions........................................... 154
19.11Logging................................................ 154
19.12Memory dump............................................ 155
19.13Assertion............................................... 155
19.14Building custom library........................................ 156
19.15Search path.............................................. 156
19.16Argument concatenation....................................... 156
19.17Dynamic function invocation..................................... 157
```
**20 Unicode 158**
20.1 Examples............................................... 158
20.2 Charset................................................ 160

**21 Standard Library 161**
21.1 AWS library.............................................. 161
21.2 Azure library............................................. 161
21.3 Cloud Insight............................................. 162
21.4 Devicons and Font Awesome library................................. 163
21.5 Google Material Icons........................................ 164
21.6 Office................................................. 165
21.7 ArchiMate............................................... 167
21.8 Miscellaneous............................................. 168


