# FTC Programming Tools

As i mentioned earlier,there are various ways to program your FTC robot.In this course,you are going to learn about them.

## Onbot Java

Onbot Java is a web based programming platform based on Java.It usually comes as the default programming language of your robot and it is used especially by rookie teams that do not use complex subsystems or additional integrations.

<figure><img src="https://i0.wp.com/pdocs.kauailabs.com/navx-micro/wp-content/uploads/2020/07/OnBotJavaAddFile.png?fit=665%2C398&#x26;ssl=1" alt=""><figcaption></figcaption></figure>

## FTC Blocks

Another way to program your robot, also based on the platform that Onbot Java uses.This method is the least used method to program a FTC robot.It is usually used by rookie teams that don't want to go into the complexity of a text based programming language.

<figure><img src="https://github.com/ftctechnh/ftc_app/wiki/images/Writing-an-Op-Mode-with-FTC-Blocks/BlocksPicture1New.jpg" alt=""><figcaption></figcaption></figure>

&#x20;



## KeyReader

The `KeyReader` interface is the base for objects that monitor an individual button or trigger on a gamepad. All `Reader` classes must implement these functions:

* `readValue()`: Reads the current value of the key, true or false, and updates the values used by the reader. Returns nothing. This must be called once every loop.
* `isDown()` : Checks if key is currently down. Will return a boolean of whether that key is pressed.
* `wasJustPressed()` : Returns boolean whether the key is pressed, but only if it was previously not pressed.
* `wasJustReleased()` : Returns boolean indicating whether the key is not pressed, but only if it was previously pressed.
* `stateJustChanged` : Returns boolean indicating that the key's value has switched.

## TriggerReader

The `TriggerReader` class implements the `KeyReader` interface. Because `GamepadEx` Triggers return a `double` , the `TriggerReader` class interprets a value of greater than `0.5` as a trigger press.

The following constructs a new Trigger Reader with a `GamepadEx` gamepad and `GamepadKeys.Trigger` trigger.

```java
TriggerReader triggerReader = new TriggerReader(
    gamepadEx, GamepadKeys.Trigger.RIGHT_TRIGGER
);
```

Below are the different methods you can use with the trigger reader.

```java
triggerReader.isDown();
triggerReader.readValue();
triggerReader.stateJustChanged();
triggerReader.wasJustPressed();
triggerReader.wasJustReleased();
```

## ButtonReader

The `ButtonReader`class implements the `KeyReader` interface. It checks if a button is pressed, released, or is down.

```java
ButtonReader reader = new ButtonReader(
    gamepadEx, GamepadKeys.Button.A
);
```

* `ButtonReader(GamepadEx gamepad, GamepadKeys.Button button)`: Constructs a new Button Reader with a `GamepadEx` gamepad and a `GamepadKeys.Button` button.
* `ButtonReader(BooleanSupplier supplier)`: Constructs a new Button Reader using the value of a boolean supplier instead of a gamepad, which allows reading value states easily without a gamepad.

```java
reader.readValue();
reader.wasJustPressed();
reader.stateJustChanged();
reader.isDown();
reader.wasJustReleased();
```

The `GamepadEx` objects actually contain `ButtonReader`s. For every `GamepadKeys.Button`, there is a matching `ButtonReader` entry in the map. It is stored internally as a `Map<GamepadKeys.Button, ButtonReader>`. This allows you to use these features just with the `GamepadEx` class.

```java
// create the gamepad
GamepadEx myGamepad = new Gamepad(gamepad1);

/** The methods for using the ButtonReaders **/
myGamepad.wasJustPressed(GamepadKeys.Button.A);
myGamepad.stateJustChanged(GamepadKeys.Button.A);
myGamepad.isDown(GamepadKeys.Button.A);
myGamepad.wasJustReleased(GamepadKeys.Button.A);

// pass the GamepadKeys.Button that you want to read
// into the method argument

// to read all buttons at once, perform a single call
myGamepad.readButtons();
/*
this is the equivalent of calling readValue() once
for all your readers
*/
```

## ToggleButtonReader

```java
ToggleButtonReader toggleButtonReader = new ToggleButtonReader(
    gamepadEx, GamepadKeys.Button.A
);
```

The `ToggleButtonReader` class extends `ButtonReader` and adds the ability to get the status of a toggle. `readValue()` needs to be run in a loop to get the state of the toggle.

`getState()` : Gets the toggle value of a button or boolean supplier.

```java
toggleButtonReader.getState();
```

### Usage

```java
GamepadEx toolOp = new GamepadEx(gamepad2);
ToggleButtonReader aReader = new ToggleButtonReader(
  toolOp, GamepadKeys.Button.A
);

while (...) {
  if (aReader.getState()) {
    // if toggle state true
  } else {
    // if toggle state false
  }
  aReader.readValue();
}
```
