# Air Desk Schema Documentation

# API Errors
```typescript
{
    message: "Name is required."
}
```





# Users

### Schema
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

### Create User
### `POST` `/api/users`

Request
```
{
    email: "zac@email.com",
    password: "password123",
    name: "zac the man"
}
```

Response `201`
> Activation email has been sent.
```
{
    userId: "62261670e18ff01d33e142bc",
    email: "zac@email.com",

    // password is always omitted.

    name: "zac the man",    // defaults to beginning
    avatarImageUrl: "",
    activated: false,
    createdAt: '2022-04-14T21:26:49.675Z'
}
```



# User Activation Confirmations

- Created when a new user signs up with email

```typescript
{
    userActivationId: string
    userId: string
    token: string       // passed in the 'activation email' link to validate this confirmation.
    createdAt: Date
}
```

### Update User Action Confirmation
### `PUT` `/api/activation/:userActivationId`

Request
```
{
   token: "vfvqMeTqnCjYyQZg45KebAJxemDX3HGf"
}
```

Response `204`
```
// success; no response
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

    hoursOfOperation: "8:00am to 10:00pm", // string

    createdAt: Date
}
```

# Work Space

- Each office location can have multiple workspots for guests to work at.
- The host of the location creates these work spots for a location

```typescript
{
    workSpaceId: string
    officeId: string    // the work space that this office belongs

    identifier: string // work space 1 or 'name'
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
    officeId: string       // the b
    stars: number         // only allow: 0 - 5
    comment: string
    createdBy: string       // user id
    createdAt: string
}
```
