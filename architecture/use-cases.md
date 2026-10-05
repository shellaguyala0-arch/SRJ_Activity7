flowchart LR

    Student[Student]
    Driver[Driver]
    Admin[Admin]

    subgraph System[Student Ride-Booking System]

        UC1((Register / Login))
        UC2((Request Ride))
        UC3((Book Ride))
        UC4((View Ride Status))
        UC5((View Transport Updates))
        UC6((Cancel Booking))

        UC7((View Ride Requests))
        UC8((Accept Ride))
        UC9((Update Ride Status))

        UC10((Manage Users))
        UC11((Manage Drivers))
        UC12((Manage Bookings))

    end

    Student --> UC1
    Student --> UC2
    Student --> UC3
    Student --> UC4
    Student --> UC5
    Student --> UC6

    Driver --> UC1
    Driver --> UC7
    Driver --> UC8
    Driver --> UC9

    Admin --> UC10
    Admin --> UC11
    Admin --> UC12
