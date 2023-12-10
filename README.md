# Holy Cows Electrical Workshop

Every match is at minimum $300,
so each match you spend dead on the field is just siphoning money.
This excelent workshop,
hosted and presented by 1538 Holy Cows,
showed some excellent techniques and systems to prevent going dark mid-match.

# Standardization

## Certification

Have mentors certify anyone working on electrical before they work on the robot.
This applies to anyone qualified last year as well.
This makes sure that everyone both knows and has the skill to follow team standards.

## CAD

Make sure to consider wiring while designing the robot.
Standardizing wiring allows for the creation of "keep-outs"(areas around the CAD model that no mechanical parts shall be)

## Points of Failure

Try to keep everything on the board at the same voltage to minimize points of failure (e.g. buck boost converters for voltage).

## Tools
Tools are consumable, standardization reduces the number of tools you need.

## Signaling & Power
Standardizing signaling protocols and power connectors allows for greater
servicability and easy validation.
Try to minimize the number of different types of wiring (e.g. running both CAN and I2C).

# Wires

## Wire gauges

- 6 gauge wire is not great for battery to PDH (4AWG is *recommended*)
- Make sure the port on the PDH fits the gauge wire you are pluggin in (small & large)
- You can use as low as 14AWG wire for a motor as long as there is a 30A breaker in the port (or up to 8AWG, but why?).

## Space-Saver

Many large teams use something called "Space Saver Wire", found on McMasterCarr.
Reportedly, this wire saves an average of 30% of the weight of regular wire.

## Stripping wire

When stripping wire *do not* twist the wire afterwards.
This makes the wire wider and does not restore the natural twist of the wire.

When stripping, follow these directions:

1. Clamp stripper and twist wire a quarter-turn.
2. Pull wire perpendicular to the stripper (This reduces fraying).
3. Just smoosh the wires together if it's a bit frayed.

# Connections

## Ferrule Connectors

Studies show that a robot in a decent collision on the field can experience up to **70 Gs**.
The most common port for a ferrule connector is only rated to 7.5 lbs of force.
This means it will rip out if the robot experiences a collision in the wrong direction.
With a ferrule connector, this will effectively destroy the port.
If there is no ferrule connector it can be recovered.

## Molex Connectors

Molex connectors are designed to be crimped, but they *can* be soldered.
When doing this, you should refer to the NASA spec.
Soldering a connector is great for things that you will reuse every year,
such as a motor controller.
Use a seperate wire with a crimped connector to connect to the PDH.

When crimping a Molex connector,
the crimper will have a deeper half and a shallow half.
The deeper half *must* be paired with the insulation piece of the connector.
Before you crimp,
use your flush cutter to squeeze the insulation wrapper on the connector.
Now you can let go of the crimp!

Holy Cows have people do ten of these in a specific time frame,
and have the crimps be inspected in order to be cleared for the year.

## Power Cabling Parts

- Main Breaker
    - 6AWG Ring Terminal ¼" Screw (MCM P/N: 7113K446)
        - This connector supports 4AWG wires
- Battery
    - 6AWG Ring Terminal #10 Screw (MCM p?n 7113K445)
        - Also supports 4AWG 
        
- Wire
    - High strand 4AWG wire
    - Recommendations
        - JSC
        - West Coast Products (future)
        - [Welding Cable](https://powerwerx.com/welding-cable-epdm)*
    - Don't Buy
        - Anything that says CCA (Copper Clad Aluminum)

For battery to PD crimping, you can use either a hammer crimper tool,
or a hydraulic crimper, which Holy Cows' claim they get the best results out of.
You can solder, but you *have* to know how to inspect.
Always check for runback on solder.
Stop adding solder when the contact point is full.
If you don't do this, the solder will run back under the insulation,
effectively turning your wire into solid-core.

## Termination

Without a good mechanical connection, you cannot have a good electrical connection.
If you have a poor mechanical connection,
this can create what's known as an HRC (High Resistance Connection).
This can happen when a connector is not fully seated, and power is being passed through a smaller surface area than the connector was designed for, and even cause fires. For you main breaker, if the ring connector wiggles at all,
it is not fully sealed. Tighten it down to about 7¼ ft lbs, or real tight.
Use a socket wrench, not a box wrench, to get some good torque on the connector.

Use locking devices, such as NordLock or Grasshopper Nuts, for a better connection.
Holy Cows use NordLock on every battery, but not on the main breaker,
since there's not enough space.
Many other teams preached the usefulness of [Grasshopper Nuts](https://www.thethriftybot.com/products/grasshopper-nut?_pos=1&_psq=battery+&_ss=e&_v=1.0).
Studies have shown they are more effective than NordLock washers.

## Power Cables

For the main breaker, after torquing the nut down, insulate the entire connection.
cover the whole connection with rubber masking tape (2M P/N 2228),
attached to the breaker.

Using 4 AWG with the

For crimping, follow these instructions:

**Important:** Make sure that the cut copper strands are level with each other,
and check that the orientation of the crimp matches with how you are connecting it.

1. Just use a box cutter to strip the 4AWG wire.
    Select the length of the base + about an eighth of an inch.
    Rotate the blade around the wire, then split the insulation paralel to the wire.
2. Bend the wire at the cut point to break the insulation,
    slicing at what doesn't want to break.
3. Pull the insulation halfway off,
    and pull a small ziptie around the bare wire to prevent fraying.
4. Pull the insulation the rest of the way off and put the ring connector on,
    pushing the ziptie back with it.
5. Use flush cutters to cut the ziptie off,
    push the ring connector all the way back,
    then crimp with your method of choice.
    Make sure that the crimp seam is on one of the flat edges.

For the SB50 connector (use the red version),
you will need to expand it if you want to use 4AWG with it.
Holy Cows made a tool for this that presses it out with an arbor press.
There is probably info on this on Chief Delphi,
but if not, Holy Cows will post dimensions with the slides.

## CAN Topologies

### CAN (Controller Area Network) (ISO 11898-2)
- Up to 1Mbit/sec
- Terminated by two 120Ω resistors
    - Resistors are used to drive the bus from the dominant state back to the     recessive state
- Tolerant to longer stubs
- Tolerand to improper bus termination/topology
- Used by: roboRIO, CTRE PDP/PCM, Rev Robotics devices, etc...
- Twined to cancel out interference

### CAN FX (CAN with Flexible Data-Rate) (ISO 11898-2 TODO find addendum)
- Up to 15 Mbit/sec
- Terminated by two 120Ω resistors
    - Resistors are used to drive the bus from the dominant state back to the     recessive state
- Intolerant to longer stubs
- Intolerant to improper bus termination/topology
- Higher speeds become less tolerant to wiring ringing and reflections.
- Allows for running two different busses.
- Used by Talon FX and CANivore.

### Physical Spec

At 1 Mbit there is a recommended maximum of 0.3 m (~12in).
Holy Cows use multiple CAN networks, one for mobility critical systems,
and one for secondary systems.

# Inspection

Make sure to inspect the reliability of things all throughout the power chain.
This means all the way from the battery to the motor (every connector).
**PULL TEST**

# Batteries

Move away from the 3-bank charger, since it does not support trickle charging.
This means if you leave a battery plugged in for a long time,
you can some back to a discharged battery.
Holy Cows uses something called an Oko charger.
When your battery charger light turns green,

Also, different metals on connectors can increase corrosion on connections.
Holy Cows replaces power cables every year, since they degrade over time.

Properly IDing your batteries can help for tracking and maintaining reliability.
Put an ID on each battery and record which matches they were used in.
Replace batteries if they have been used for more than 2 years.

Batteries want to be cool while being charged, and warm when being used.
The Holy Cows are starting to use a battery warming blanket next year.

[BatteriesPlus](https://www.batteriesplus.com/productdetails/battery/sla-sealed-lead-acid/12/wkdc12=20nb) is a great place to buy batteries,
and from the Holy Cows' experience,
they will often give a discount if you let them know you are with a school.

# Hardening devices

## Preventing internal shorts

OpenMesh radios have a big metal plate inside to prevent emissions on restricted frequencies.

