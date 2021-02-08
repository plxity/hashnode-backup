## Hangman - A fun game to see how much people know you.

## Introduction

[Hangman game](https://hangman-multiplayer.plxity.vercel.app/) is my submission for @[Hashnode](@hashnode) and Vercel Hackathon under the category - **Social**. It is a small application/game to play with your friends. I hope you'll like it. 😄

## Hangman
It is a fun application based on actual **Hangman game** to find out how much your friends know you. 
It provides a platform for the user to create a quiz for their friends and share the link with them to play. Based on correct answers for each question, the score will be generated and it will be stored in the database. User can view the score of all the people who played the game. 

**Link** -  [Hangman Game](https://hangman-multiplayer.vercel.app/) 


**GitHub** - [I'm trying to improve the UI/UX. Once I feel it is up to the mark, I'll open-source the project.]()

## 💡 The Idea 

I always wanted to build an application in the category of social but used to drop the idea. When I heard about Hashnode hackathon I thought of pushing myself and finally build something in this domain. I came across a hangman game on the internet a few months back. Then I saw a tutorial on building this game by **Traversy media** where he explained how to build this game using VanillaJS. I watched that tutorial and build that. At the same time, I got an idea to integrate a feature to play with friends in a quiz format. So I thought of building a Hangman game in this format.

##  👨🏻‍💻 Tech stack

#### Frontend
1. HTML
2. CSS
3. ReactJS

#### Backend
1. NodeJS
2. ExpressJS
3. MongoDB

Whenever I build a Full-Stack application, I always start with the backend code because it gives me the freedom to change the flow of the application if I want to. Initially, I started writing code for the backend using ExpressJS and storing all the information in MongoDB. Once I finished the code for backend, I tested the API using postman. After that, I started with the Frontend part using ReactJS. I always like to code CSS from scratch so this time also I preferred that.  

## 🚗 Development Journey and challenges

While building a Full-Stack application, the most important thing which you have to decide is the database design. I used a NoSQL database for this application. The scheme looks like this -
```
const UserSchema = new Schema({
  name: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: false,
  },
  questions: [
    {
      questionValue: {
        type: String,
        required: true,
      },
      answerValue: {
        type: String,
        required: true,
      },
      hintValue: {
        type: String,
        required: false,
      },
    },
  ],
  participants: [
    {
      name: {
        type: String,
        required: true,
      },
      score: {
        type: Number,
        required: true,
      },
    },
  ],
});
```
Building a backend server for this application was not that tough. The major challenges I faced were on the frontend part. I didn't use ```Redux``` in this application so it was difficult for me to maintain so many states parameters. But I found an effective method to deal with it by reading blogs and finding solutions on  StackOverflow.

## ✅ Final Application 

The final application looks like this -

- This is the landing page of the application.

![Screenshot 2021-02-02 at 1.04.43 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612246368722/hKZMqke6L.png)

- When a user clicks on ```Create Game```, it will be redirected to a new route where the user will have to enter the questions they want to ask people.



![Screenshot 2021-02-02 at 11.47.17 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612246647843/lYUDVLATy.png)

- After filling this form user will be redirected to a page where **two different links** will be generated and you can copy them on the clipboard.

**1.  First link** - You can share this link with other people whom you want to attempt the quiz.

**2.  Second link** - This link is used to view the responses of your friends. It will show their name and score.


![Screenshot 2021-02-02 at 11.50.38 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612247114974/Z2FcFFg-3.png)

- When a person visits a link shared by you, the game screen will look like -


![Screenshot 2021-02-02 at 2.02.31 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612254908822/oa6chV3SR.png)

- Whenever a user enters a wrong letter, that hangman starts **growing** on every wrong letter. A user will be given 6 chances for answering one question. After 6 wrong attempts, the user will be moved to a new question. 




![Screenshot 2021-02-02 at 2.00.25 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612254933325/XUrlKNI30.png)

- After completion of the game, it will be redirected to a page to submit your score. 


![Screenshot 2021-02-02 at 12.03.11 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612247601349/C-V5ZYO_r.png)


## ⚡️ Try it out

The link for the application is - [Hangman](https://hangman-multiplayer.plxity.vercel.app/). Please try it out and share the link with your friends. Let me know what can be added to this application to improve it. 🚀 Looking forward to feedback from your side. ⚡️


-----------------------------------------------------------------------------------------------------------

I always try to share my learning with the community. Connect to me on [Twitter](https://twitter.com/apoorv_taneja), [GitHub](https://github.com/plxity) or [LinkedIn](https://www.linkedin.com/in/apoorvtaneja/). Subscribe to my newsletter for the latest blog posts. 💙

Happy Learning ⚡️