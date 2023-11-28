# Gladiator Robotics Java Robot Code Style Guide
Refer to [Java Style Guide](https://google.github.io/styleguide/javaguide.html) for more in-depth style guidelines.
## Table of Contents
- [Code Styling](#Code-Styling)
    - [General Guidelines](#General-Guidelines)
    - [Naming Conventions](#Naming-Conventions)
    - [File Structure](#File-Structure)
    - [Code Documentation](#Code-Documentation)
- [Example](#Example)

## Code Styling
### General Guidelines
- One statement per line.
- No while(true) {} loops.
- No public variables, use getters and setters.
- Exactly one top level class definition in file. 
- WPILib will automatically generate with 2 space indents, switch to 4 spaces for all the code you write.
- Exactly one space before opening brace, no new line.
- Line break before closing brace.
- Horizontal alignment not required.
- No implicit return.
- Commands should always have a name (see example below).
- Use radians as default angle messure.


### Naming Conventions
- File Names - PascalCase
- Classes/Enum/Interfaces - PascalCase
- Methods - camelCase
- Variables - camelCase
    - Constants - kPascalCase
    - Members Variables - m_camelCase

### File Structure
1. Package statements
2. Import statements (new lines seperate vendors)
3. Top level class declaration

### Code Documentation
- Code should be readable, but if it isn't, document it!
- Follow the documentation in the example below so VSCode can read it and use to give info when hovering functions

## Example
```java
/** 
* Represents a command-based swerve drivetrain
*/
public class SwerveSubsystem extends SubsystemBase {
    /**
    * @return a Command object that drives with given joystick inputs
    * @param joyLeftX left joystick x value supplier
    * @param joyLeftY left joystick y value supplier
    * @param joyRightX right joystick x value supplier
    * @param fieldRelative drive fieldRelative supplier
    */
    public Command getDriveWithJoystickCommand(
        DoubleSupplier joyLeftX,
        DoubleSupplier joyLeftY,
        DoubleSupplier joyRightX,
        BooleanSupplier fieldRelative) {
        return this.run(() -> {
            // get joystick axises
            double vx = MathUtil.applyDeadband(joyLeftX.getAsDouble(), Constants.DriveTeamConstants.kJoystickDeadzone);
            double vy = MathUtil.applyDeadband(joyLeftY.getAsDouble(), Constants.DriveTeamConstants.kJoystickDeadzone);
            double rot = MathUtil.applyDeadband(joyRightX.getAsDouble(), Constants.DriveTeamConstants.kJoystickDeadzone);

            // apply max speeds
            vx *= m_maxSpeed;
            vy *= m_maxSpeed;
            rot *= m_maxAngularSpeed;

            drive(vx, vy, rot, fieldRelative.getAsBoolean());
        }).withName("DriveWithJoystickCommand);
    }
}
```
