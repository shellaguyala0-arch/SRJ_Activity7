# Diagram 2 — C4 Container

```mermaid
C4Container

title Diagram 2 - C4 Container: SRJ Student Ride Booking (MVP)

Person(student, "Student", "Books rides to school")
Person(driver, "Tricycle Driver", "Accepts rides and updates trips")
Person(coordinator, "Coordinator", "Manages drivers and reviews metrics")

System_Boundary(srj, "SRJ Ride Booking") {

    Container(web, "Web App (UI)", "Next.js / React in the browser", "Booking, driver and coordinator pages")

    Container(api, "API", "Next.js route handlers on Node.js", "Applies booking rules, matches drivers and sets trip status")
}

ContainerDb(database, "Database", "PostgreSQL", "Stores users, bookings, location updates and notifications")

System_Ext(maps, "Maps Provider", "External System", "Distance and ETA")
System_Ext(notification, "Notification Provider", "External System", "Email or SMS alerts")

Rel(student, web, "Books and follows rides using", "HTTPS")
Rel(driver, web, "Accepts rides and updates trips using", "HTTPS")
Rel(coordinator, web, "Manages drivers and reads metrics using", "HTTPS")

Rel(web, api, "Sends booking, trip and tracking requests (status polled every few seconds)", "HTTPS/JSON")

Rel(api, database, "Reads and writes records", "SQL over TCP (TLS)")
Rel(api, maps, "Gets distance and ETA", "HTTPS/JSON")
Rel(api, notification, "Sends booking alerts", "HTTPS/JSON")
