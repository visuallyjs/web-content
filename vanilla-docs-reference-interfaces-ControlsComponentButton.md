ControlsComponentButton

Definition of a button in the controls component.

| Name    | Type                        | Description                                                                |
| ------- | --------------------------- | -------------------------------------------------------------------------- |
| class   | string                      | css class to set on the button's DOM element                               |
| handler | (e:Event, id:string) => any | Handler for clicks (taps) on this button.                                  |
| id      | string                      | Button's id.                                                               |
| mode?   | string                      | Optional UI mode to set when the button is pressed                         |
| title   | string                      | Set as the button's DOM element's label attribute (a tooltip, effectively) |
