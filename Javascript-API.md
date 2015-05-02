## Events

Kloudspeaker events can be listened

    kloudspeaker.events.addEventHandler(fn, eventId);

where `fn` is handler function (called with one parameter, event) and `eventId` string for event identifier.

for example, to listen session start event

    kloudspeaker.events.addEventHandler(function(e) {
        // add event logic
    }, "session/start");

