# Button press detector for ESP8266 SDK

This repo is forked from https://github.com/craftmetrics/esp32-button. It implements a version of [THE ULTIMATE DEBOUNCER(TM) from hackaday](https://hackaday.com/2015/12/10/embed-with-elliot-debounce-your-noisy-buttons-part-ii/
).

It can monitor multiple pins, and sends button events over a queue for your application to process.

## Available input GPIO pins

Only the following pins can be used as inputs on the ESP8266:

0-19, 21-23, 25-27, 32-39


## Example Usage

```
button_event_t ev;
QueueHandle_t button_events = button_init(PIN_BIT(BUTTON_1) | PIN_BIT(BUTTON_2));
while (true) {
    if (xQueueReceive(button_events, &ev, 1000/portTICK_PERIOD_MS)) {
        if ((ev.pin == BUTTON_1) && (ev.event == BUTTON_DOWN)) {
            // ...
        }
        if ((ev.pin == BUTTON_2) && (ev.event == BUTTON_DOWN)) {
            // ...
        }
    }
}
```

## Event Types

### BUTTON_DOWN

Triggered when the button is first considered pressed.

Also triggered every 50ms during a long press.

### BUTTON_UP

Triggered when the button is considered released. In most cases you can use either the UP or DOWN event for your application, and ignore the other.
