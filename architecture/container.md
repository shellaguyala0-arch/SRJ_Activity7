flowchart TB

    Student["Student<br/>Books and follows rides"]
    Driver["Tricycle Driver<br/>Accepts rides and updates trips"]
    Coordinator["Coordinator<br/>Manages drivers and reviews metrics"]

    subgraph SRJ["SRJ Ride Booking"]
        Web["Web App (UI)<br/><br/>Next.js / React in browser<br/>Booking, driver and coordinator pages"]

        API["API<br/><br/>Next.js route handlers on Node.js<br/>Applies booking rules, matches drivers<br/>and persists trip status"]
    end

    DB[("Database<br/><br/>PostgreSQL<br/>Users, bookings, locations,<br/>notifications")]

    Maps["Maps Provider<br/>External System<br/>Distance and ETA"]

    Notify["Notification Provider<br/>External System<br/>Email or SMS alerts"]

    Student -->|"Books and follows rides<br/>[HTTPS]"| Web
    Driver -->|"Accepts rides and updates<br/>trips [HTTPS]"| Web
    Coordinator -->|"Manages drivers and reads<br/>metrics [HTTPS]"| Web

    Web -->|"Booking, trip and tracking requests<br/>[HTTPS/JSON]<br/>Polling every few seconds"| API

    API -->|"Reads and writes records<br/>[SQL over TCP/TLS]"| DB
    API -->|"Gets distance and ETA<br/>[HTTPS/JSON]"| Maps
    API -->|"Sends booking alerts<br/>[HTTPS/JSON]"| Notify

    classDef person fill:#0B4F8A,color:white,stroke:#083B66;
    classDef container fill:#4A90D9,color:white,stroke:#155A91;
    classDef database fill:#3F8ED0,color:white,stroke:#155A91;
    classDef external fill:#777,color:white,stroke:#555;

    class Student,Driver,Coordinator person;
    class Web,API container;
    class DB database;
    class Maps,Notify external;
