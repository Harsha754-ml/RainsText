# Rainmeter Skin: Time in Words

A simple, clean Rainmeter skin that displays the current system time in a human-readable word format (e.g., "It is twenty five past ten AM").

![screenshot](https://i.imgur.com/your-screenshot.png)  
*(Note: You can replace this with a real screenshot after loading the skin.)*

## Features

-   **Human-Readable Time**: Converts numeric time into words.
-   **Handles All Cases**: Correctly formats for "o'clock", "past", "to", "quarter past", "half past", and "quarter to".
-   **AM/PM Support**: Displays AM or PM as appropriate.
-   **Customizable**: Easily change the font, color, size, and position.
-   **Efficient**: Updates only once per minute to conserve system resources.

## Installation

1.  **Download**: Download the `.rmskin` package from the [Releases](https://github.com/your-username/your-repo/releases) page (or clone this repository).
2.  **Install**: Double-click the `.rmskin` file. The Rainmeter Skin Installer will open. Click the **Install** button.
3.  **Load Skin**:
    -   Open your Rainmeter manager.
    -   Navigate to `TimeInWords` > `TimeInWords.ini`.
    -   Right-click and select `Load` (or double-click it).
    -   The skin will appear on your desktop.

## How the Time-to-Words Logic Works

This skin uses only built-in Rainmeter measures and meters to convert time to words, with no external scripts.

1.  **Core Time Measures**:
    -   `[MeasureHour]`, `[MeasureMinute]`, `[MeasureAmPm]` fetch the raw numbers (e.g., `10`, `25`, `AM`).
    -   `[MeasureNextHour]` calculates the upcoming hour for phrases like "ten to three".

2.  **Number-to-Word Conversion**:
    -   A series of `Calc` measures (`[MeasureHourWord]`, `[MeasureMinuteWord]`, etc.) use the `Substitute` property to map numbers to their corresponding English words (e.g., `10` becomes `"ten"`).

3.  **Conditional Phrase Logic**:
    -   The skin determines which phrase to use based on the minute of the hour.
    -   A set of `Calc` measures, one for each condition (e.g., `[MeasurePhrasePast]`, `[MeasurePhraseQuarterTo]`), checks if the current minute matches its rule using `IfCondition`.
    -   For example, `[MeasurePhraseQuarterPast]` only produces text if `[MeasureMinute]` is exactly `15`. All other conditional measures produce an empty string.

4.  **Final Assembly**:
    -   `[MeasureFinalTimeText]` concatenates the output of all the conditional phrase measures. Since only one of them can be active at any given time, the result is the single, correct time phrase.
    -   The final `[MeterTime]` string meter then combines this phrase with "It is" and the AM/PM measure to display the complete sentence.

## Customization

You can easily customize the skin's appearance by editing the variables file.

1.  **Find the Variables File**:
    -   Right-click the skin on your desktop.
    -   Go to `Time in Words` > `Edit variables`.
    -   This will open the `TimeInWords-Rainmeter\@Resources\Variables.inc` file in your default text editor.

2.  **Editable Variables**:

    -   `FontName`: The name of the font you want to use.
    -   `FontColor`: The color of the text in `R,G,B,A` format (Red, Green, Blue, Alpha/Transparency).
    -   `FontSize`: The size of the text.
    -   `SkinX`, `SkinY`: The position of the skin on your desktop. Can be a pixel value (e.g., `100`) or a percentage (e.g., `50%`).
    -   `SkinAnchor`: Sets the anchor point for positioning. `C` means center, `TL` means top-left, etc.

3.  **Save and Refresh**:
    -   Save the `Variables.inc` file after making your changes.
    -   Right-click the skin on your desktop and select `Refresh` to see your changes applied.
