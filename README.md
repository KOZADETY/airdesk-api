# Air Desk Schema Documentation

# Users

```typescript
{
    userId: string
    email: string
    password: string
    name: string
    avatarImageUrl: string // must be url to image
    
    // look into apple and google sign on

    activated: boolean // default false
    createdAt: Date
}
```

# User Activation Confirmations

- Created when a new user signs up with email

```typescript
{
    userId: string
    token: string       // passed in the 'activation email' link to validate this confirmation.
    createdAt: Date
}
```

# Office

- A 'host' user can create a location that has space to lease out - like desks/tables.

```typescript
{
    officeId: string
    name: string        // "The Crypt of Lord Zaros"
    description: string // "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget"

    images: [
        'https://someserver.com/file/a34f34f34fa4faigg.jpg',
        'https://someserver.com/file/xca034jva340v34va.jpg',
        'https://someserver.com/file/039a4341l2dk10dle.jpg'
    ]

    address: {
        country: string
        state: 'NC' // two character state code
        city: string
        fullStreet: string // text area, allows user to input any extra numbers or identifiers
        zipcode: string
    }

    amenities: [
        'coffee',
        'standupDesk',
        'highSpeedWifi',
        'kitchen'
    ]

    petsAllowed: boolean

    hoursOfOperation: {
        // TBD
    }

    createdAt: Date
}
```

# Work Space

- Each office location can have multiple workspots for guests to work at.
- The host of the location creates these work spots for a location

```typescript
{
    workSpaceId: string
    officeId: string

    identifier: string // work space 1
    notes: string // text area

    maxNumberOfOccupants: number // must be greater than zero. e.g. 1 would be for a single desk area, 5 would be for a large free room.
    guestsAllowed: boolean

    // at least 3
    images: [
        'https://someserver.com/file/a34f34f34fa4faigg.jpg',
        'https://someserver.com/file/xca034jva340v34va.jpg',
        'https://someserver.com/file/039a4341l2dk10dle.jpg'
    ]

    createdAt: Date
}
```

# Work Space Reservations

- A user can 'reserve' a space to work at

```typescript
{
    workSpaceReservationId: string
    workSpaceId: string  // spot being reserved
    userId: string      // user creating the reservation

    // to calculate 'days' length
    reservationStartDate: Date
    reservationEndDate: Date

    createdAt: Date
}
```


# Work Space Review
- A guest user can leave a review for a workspace
```typescript
{
    reviewId: string
    officeId: string
    stars: number         // only allow: 0 - 5
    comment: string
    createdBy: string       // user id
    createdAt: string
}
```
