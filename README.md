# Simplified-Plane-Physics-Unity
Simplified Plane Physics in Unity3D/C#.

## Plane setup
The Plane consists of an engine and four airfoils (the two wings and the horizontal and vertical stabilizers)
- the plane's center of gravity is at (0, 0, 0)
- the left wing is at (-wingX, 0, 0). (That is, its mass is modeled as a point mass at that location, and its lift force is modeled as a point force at that location.
- the right wing is at (wingX, 0, 0)
- the horizontal and vertical stabilizers are at (0, 0, tailSize)
- the engine is somewhere on the negative Z axis. (Its location is determined

by the fact that the center of gravity is at (0, 0, 0).) Its mass, too, is modeled as a point mass and its thrust force as a point force at the same location.

### Angle of attack (AOA)
An airfoil's attack vector is defined as followed:
- The left wing's attack vector is (0, sin(leftWingInclination), -cos(leftWingInclination)).
- The right wing's attack vector is (0, sin(rightWingInclination), -cos(rightWingInclination)).
- The horizontal stabilizer's attack vector is (0, sin(horStabInclination), -cos(horStabInclination)).
- The vertical stabilizer's attack vector is (-sin(verStabInclination), 0, -cos(verStabInclination)).

### Forces on plane
An airfoil's normal as the cross product of its axis vector and its attack vector.

We define an airfoil's projected airspeed vector as its airspeed vector (its velocity minus the wind velocity) projected onto the plane perpendicular to its axis vector. We define its projected airspeed as the size of its projected airspeed vector. We define its angle of attack as -atan2(S . N, S . A), where S is the projected airspeed vector, N is the normal, and A is the attack vector. 

The forces operating on the plane, in plane coordinates, are the following:

- Gravity applies to each of the four point masses
- The engine thrust force vector is (0, 0, -thrust)
- Each airfoil generates a lift force N . liftSlope . AOA . s^2, where N is the normal, AOA is the angle of attack, and s is the projected airspeed. No other forces operate on the Plane; in particular, there is **no drag.**

## plane's parameters

    /** The world's gravitational constant (in N/kg). */
    float gravity;
    /** Distance between the drone's center of gravity and the point where the
    wings' mass and lift are located. */
    float wingX;
    /** Distance between the drone's center of gravity and the point where the tail mass and the lift generated by the horizontal and vertical stabilizers is located. */
    float tailSize;
    /** Mass of the engine. The engine is located in front of the drone's center of gravity. */
    float engineMass;
    /** Mass of the left wing. Equals the mass of the right wing. Modeled as being located in a single point. */
    float wingMass;
    /** Mass of the tail. Modeled as being located in a single point. */
    float tailMass;
    /** Maximum forward engine thrust. (Minimum thrust is zero.) */
    float maxThrust;
    /** Maximum magnitude of the angle of attack of all four airfoils. If during simulation an airfoil's angle of attack exceeds this value, the simulator may report an error and abort the simulation. */
    float maxAOA;
    /** The liftSlope value for computing the lift generated by a wing. */
    float wingLiftSlope;
    /** The liftSlope value for the horizontal stabilizer. */
    float horStabLiftSlope;
    /** The liftSlope value for the vertical stabilizer. */
    float verStabLiftSlope;
    /** thrust of the drone. */
    float thrust;
    /** inclination of the left wing */
    float leftWingInclination;
    /** inclination of the rightwing */
    float rightWingInclination;
    /** inclination of the horizontal stabelizer */
    float horStabInclination;
    /** inclination of the vertical stabelizer */
    float verStabInclination;
