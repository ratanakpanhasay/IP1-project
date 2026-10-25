# Week 03 — Answers

## 1. Why should we not use the array index as `:key`?

Using the array index as `:key` can cause Vue to reuse the wrong component when a list is filtered or reordered. If a card has local state, that state may appear on a different event. Using each event's unique ID helps Vue track the correct component.

## 2. Why is `visible` a computed property instead of a function?

A computed property caches its result and recalculates when its reactive dependencies change. A function called in the template runs again whenever the component renders. Using `computed` is useful for filtering because Vue can reuse the result until the search text, category, or events change.

## 3. Why does EventCard emit `book` instead of changing `event.booked`?

Props should be treated as read-only because the parent owns the event data. Emitting a `book` event lets the parent check seat availability and update the booking state. This also makes EventCard easier to reuse.

## 4. Why does destructuring `booked` from a reactive object cause a problem?

Destructuring a primitive property from a reactive object separates its value from the reactive object's property. Therefore, changing the separate variable does not update `event.booked`. Also, declaring `booked` with `const` means it cannot be reassigned with `booked++`.

## 5. Where does `myBookings` live, and why?

`myBookings` lives in `App.vue` because it manages the application's booking state. EventCard emits booking requests, and EventList forwards those events to App.vue. Keeping the state in the parent allows the application to update the booking count, prevent overbooking, and persist bookings across page reloads.
