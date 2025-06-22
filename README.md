## Morning Burrito - mobile app for creatives
This was my final group project at Le Wagon. Primarily a mobile app, it is an app in the style of Duolingo where instead of daily language lessons, you do activities that are meant to inspire creativity; for example, writing a haiku based on a prompt or drawing a picture based on recordings of some sounds outside. 

## Teammates
- [Alex](https://github.com/alexandertan527)
- [Patrick](https://github.com/patricka03)
- [Joanne](https://github.com/Andrejo42)
- [Paul](https://github.com/paulosagie15)

## Goals
- To create a full-stack application from conception to finished product.
- Work as a team, learning about and utilizing software engineering best practices and working in an agile way. 

## Tech Stack
- Ruby on Rails
- HTML5
- SCSS
- JavaScript
- Bootstrap
- Git
- Github
- PostgreSQL
- Figma

## Login
You can access the home and new idea page without logging in, as I wanted anyone to be able to use the app for some quick inspiration. To save a song however, you must log in. I utilised Devise for authentication. If you do not want to create a user, please use these login details instead:

- Email: tester@testing.com
- Password: gimmeatester

## Process
I started with: 
- a rough sketch of what I wanted the app to look like. This included pictures and a description of what I wanted the user to receive from the app (a randomly generated song idea).
- the database schema.



Following this, I started setting up the Rails project and implementing the backend. To be continued...


## Reflections
I learnt a lot about the whole process of making a full-stack application, in particular the difference between server-side and client-side, and how the two communicate with one another. One challenge I faced was figuring out how to randomly generate the instrument without constantly updating the database, while still ensuring that the backend recognized the song and instrument data when saving a new song idea. This led me to use sessionStorage, as I didn’t want or need the randomly generated data to persist across browser sessions. It was a good fit for holding temporary client-side data.


- Functions like randomTime, randomMood, etc, live in the Stimulus controller and generate specific song elements.
- As Instrument and Song were two separate models, I separated the sessionStorages too.
- To know if it was working, I put a simple console.log of the generated data. 

However, I realised that I still needed a way to save the generated data. I came upon a solution by accident, when I was trying to work out the logic of allowing a user to name their saved song idea - this would not work originally, as the validations on the Song model were not passing without a value for mood, key, etc being saved as well. As I was using Simple Form, I decided to use hidden_inputs for each of the song elements. This aligned perfectly with what I was trying to achieve with sessionStorage, as I could now send the data through as a hidden form field. 


In the saveSong function, I could now use AJAX and the fetch API to send it through to my songs controller in Rails. This approach let me bridge the gap between the client-side generation and the server-side persistence of data.


Another challenge was establishing the relationships between the different tables: Songs and Instruments. I realised early on that they had a many-to-many relationship, which would require a joins table called SongInstruments. After grappling with this for a couple of days, I decided to stop and sketch out the different relationships as you can see in the image below. This helped me to visualise the Active Record query methods and is something I now do before every new project.


## Future Additions
I'd like to add the ability to have multiple suggested instruments, as well as use the OpenAI api to suggest songs for inspiration. I attempted to incorporate the OpenAI API (as seen in my source code), however the songs it would suggest for inspiration were incorrect. For example, when prompting it to suggest songs in 9/8 time signature, it was adamant that 'Solsbury Hill' by Peter Gabriel was in 9/8, despite it being one of the most famous examples of a song in 7/8. Because of this, I decided to not deploy with this error intact, and to dedicate more time to work out why this is happening.
