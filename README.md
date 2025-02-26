# Project's name REST API
## Description

This is a the backend repository for the React application `CoBrain`.

---

## Instructions

When cloning the project, change the <code>sample.env</code> file name for <code>.env</code>. The project will run on **PORT 8000**.

Then, run:
```bash
npm install
```
## Scripts

- To start the project run:
```bash
npm run start
```
- To start the project in development mode, run:
```bash
npm run dev
```
- To seed the database, run:
```bash
npm run seed
```
---

## User stories (MVP)

- User can sign up and create and account.
- User can login.
- User can log out.
- User can create a Knowledge.
- User can edit its Knowledge.
- User can delete its Knowledge.

---

## User stories (Backlog)

- User can search for a category of Knowledge and location.
- User can see its vote history.
- User can filter Knowledge by Music.
- User can filter Knowledge by Time.

## Models

### User

Users in the database have the following properties:

```js
const userSchema = new Schema(
  {
    email: {
      type: String,
      unique: true,
      required: true
    },
    hashedPassword: {
      type: String,
      required: true
    },
    username: {
      type: String,
      required: true 
    },
    role: {
      type: String,
      enum: ['user', 'admin'],
      default: 'user'
    },
    profileImage: {
      type: String,
      default: ""
    },
    country: {
      type: String,
    },
    city: {
      type:String,
    },
    contactInfo: {
      type: String,
    },
    description: {
      type: String,
    },
  },
  {
    timestamps: true
  }
);
```
### Knowledge

Knowledge in the database have the following properties:

```js
const knowledgeSchema = new Schema (
    {
        category: {
            type: String,
            enum: [
                "Music",
                "Cooking",
                "Health",
                "Sport",
                "Crafts",
                "Circus",
                "Languages",
                "Animals",
                "Others",
            ],
            required: [true, "Category is required"],
        },
        userId: {
            type: Schema.Types.ObjectId,
            red: "User",
            required: true
        },
        title: {
            type: String,
            required: [true, "Title is required."],
        },
        knowledgeImage: {
            type: String,
            default:"https://thumbs.dreamstime.com/z/conexi%C3%B3n-del-cerebro-32729762.jpg",
            required: [true, "Image is required."],
        },
        timeOfActivity: {
            type: Number,
            default: 0,
            required: [true, "Time in hours and/or minutes approximately is required."]
        },
        location: {
            type: String,
        },
        description: {
            type: String,
            required: [true, "Description is required."]
        },
        contactMe: {
            type: String,
            required: [true, "Description is required."]
        },
    
    },
    {
        timestamps: true
    },
);
```

### Review

Review in the database have the following properties:

```js
const reviewSchema = new Schema(
    {
        userId: {
            type: Schema.Types.ObjectId,
            ref: "User",
            required: true
        },
        imageUrl: {
            type: String,
            required: true
        },
        title: {
            type: String,
            required: true
        },
        description: {
            type: String,
            required: true
        }
    }
);
```

### Favorite

Favorite in the database have the following properties:

```js
const favoriteSchema = new Schema(
    {
        userId: {
            type: Schema.Types.ObjectId,
            ref: "User",
            required: true
        },
        knowledgeId: {
            type: Schema.Types.ObjectId,
            ref: "Knowledge",
            required: true
        }
    },
    {
        timestamps: true
    }
);
```


---

## API endpoints and usage 

| Action              |Method| Endpoint                  | Req.body                          |Private/Public     |
|---------------------|------|----------------------     |---------------------------------  |-----------------  |
| SIGN UP user        | POST | /auth/signup              | { username, email, password }     |      Public       |                 
| LOG IN user         | POST | /auth/login               | { email, password }               |      Public       |                  
| GET logged in user  | GET  | /auth/me                  |                                   |      Private      |
|                                                                                                                |
| GET all knowledges  | GET  | /knowledges/              |                                   |      Public       |
| GET one knowledge   | GET  | /knowledges/:knowledgeId  |                                   |      Private      |
| POST one knowledge  | POST | /knowledges/              |                                   |      Private      |
| EDIT konwledge | PUT| /knowledges/:knowledgeId| {category,title,knowledgeImage,timeOfActivity,location,description,contactMe}| Private|
|DELETE knowledge     |DELETE| /knowledges/:knowledgeId  |                                   |      Private      |
|                                                                                                                |
| EDIT User | PUT| /users/edit| {email,hashedPassword,username,profileImage,country,city,contactInfo,description}| Private|
| DELETE User         |DELETE| /users/delete             |                                   |      Private      |
| DELETE User (Admin) |DELETE| /users/:userId/delete     |                                   |   Private/admin   |
|                                                                                                                |
|

---

## Useful links

- [Presentation slides](https://slides.com/ricardmontfortromero/cobrain/edit)
- [Frontend repository](https://github.com/RicardMontfort90/frontend-template-m3)
- [Frontend deploy](https://github.com/RicardMontfort90/frontend-template-m3)
- [Deployed REST API](https://cobrain.netlify.app/)
