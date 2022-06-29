## getReferral - Manage referrals easily and apply at one click for openings.


![Group 89.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656456599223/sbXp8xOja.png align="center")


## Problem statement 🛠

#### Job creator perspective 🕵️‍♀️

Imagine posting about a **hiring post** or **referral job opening** on **Twitter or LinkedIn** and receiving 100s of resumes to go through..sounds so tiring and tedious, right? [GetReferral](https://get-referral.vercel.app/) solves this for you. It is a platform where you can post a **job opening for referral**, **share the apply link**, receive as many responses as you possibly can and **filter** the responses in accordance with your **preference** and **hire the best talent.**

#### Candidate perspective 🧑‍🎓

We not only allow posting a job opening but also applying at an easy pace via [Peerlist](https://peerlist.io/). It is one-stop for all your proof of work. Just enter your Peerlist username and boom, you just applied for a referral. **No effort** of **emailing resumes** and **filling boring google forms** again and again 

### Important Links

- Link - [getReferral](https://get-referral.vercel.app/)

- Design link - [Figma](https://www.figma.com/file/7mptGEX3U75LTnuZb8R8pA/Hackathon?node-id=20%3A33)

- GitHub - [Repository](https://github.com/plxity/getReferral)

> As per our market research, no product like this exists that solves the problem of managing 100s messages for job referrals and filtering the best profiles.


![Screenshot 2022-06-29 at 4.50.44 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656458460035/vziz858hX.png align="center")


### key features ⚡️

- **Prevent** a lot of DMs
- Chances of **best profiles getting skipped** are reduced.
- **Filter profiles** with a lot of **flexible parameters**
- **Reduce duplicate entries,** saves time
- **Easy one-click** apply for candidates


### Design aspect of our product 💅

We wanted to keep the design minimalistic and understandable. Our idea of design instinctively included simple and lucid copywriting as well as content writing. Our goal was clear:

- Understandable Copywriting
- Simple yet Sleek Design
- A single CTA to make it easy
- Clean and effortless interactions to not make the site laggy

The job creation form doesn’t have unnecessary input fields. We kept it precise and to the point to improve the experience and make it less **time-consuming** and **more valuable**.


### Let's come to the code aspect now 🧑‍💻

After brainstorming on the architecture of the application, we decided to go forward with the **NoSQL** database (MongoDB) and **NextJS** on the frontend.

We'll now talk in detail about both Frontend and Backend respectively.

#### Frontend 

NextJS is really a great framework when have to build an application without focusing much on routing, performance, Client-side fetching, managing CSS and project structure.

After deciding to go forward with NextJS, we had to integrate an authentication layer and Next-Auth is the best option to consider for this. It provides OAuth for almost all the providers. 

We decide to integrate the following OAuth providers into our application. 

- **Google Login** (Most of the users have accounts on google)
- **LinkedIn Login** (Best option for professionals)

Moving ahead, we needed reusable common UI elements for our application like input fields, buttons, modals etc.

We decided to build `Input`, `Buttons` and `Cards` from scratch on top of `styled-components`. And use `Radix-UI` for accessible `modals`.

Now comes the most interesting part, which is showing the tabular format of responses that the user has received for the job opening and no library other than `react-table` can do this job in a sleek, efficient and performant way. 

React Table provides all the features, utilities and customisation for dealing with tabular data. We integrated **soring, filtering and fuzzy search** features easily in our table so that users can filter out the **best responses ** as per the requirement. 

And for making API calls and managing data in MongoDB we used NextJS serverless function. 


#### Backend

We used a NoSQL database (MongoDB) by **Linode** to store all the information regarding job openings and responses received. 

Considering the architecture and requirements, we wanted an object-based model to store our data.

We created two schemas -

- **Profiles** - To store information about the user and the job openings they have created

- **Responses** - To store information regarding the responses received on job openings. 


### Application overview 📎

- We provide Google and LinkedIn sign-in options to our users and get access to the dashboard.

![Screenshot 2022-06-29 at 4.52.22 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656458592946/q-yvgYryf.png align="center")

- Once you log in to our application, you will find 2 CTAs. One for viewing responses and the second for creating a job opening. 

![Screenshot 2022-06-29 at 4.36.14 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656457618015/BEWaCGAlL.png align="center")

- After clicking on `Create a job opening`, a form would appear to fill in the basic details about the job. We have used HTML form validation here. 

![Screenshot 2022-06-29 at 4.37.36 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656457673155/cARS1gxII.png align="center")

- Once the application is created, you would get a **shareable link** for the people who want to apply for this job.

- After the responses are received, you can view them in the `View Application` screen. A **tabular data ** with **unique values** would be displayed. The user would get a lot of filtering and sorting option to find the best talent.


![Screenshot 2022-06-29 at 4.42.05 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656457947609/JvOLz-dya.png align="center")

- Now if a candidate wants to apply for a job opening after receiving a link

![Screenshot 2022-06-29 at 4.47.36 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656458268732/hfYi-Zvjp.png align="center")


- They would just have to click on the apply CTA, **enter email and Peerlist username** and boom, you just applied for a job opening in **2 steps**. We would fetch all the details from your peerlist profile and submit the response.  No effort of **sending emails** with resumes and **filling google forms** for referrals. 

![Screenshot 2022-06-29 at 4.48.52 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656458342967/XmOVgdeVu.png align="center")


![Screenshot 2022-06-29 at 4.54.39 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656458788206/hRxSAroo6.png align="center")


### Upcoming features 🎉

- Feature to **bookmark profiles** in the response table to save them for future
- Dashboard for candidates to **view previous application**
- **Referral rate score** for job creators to get a better idea.
- Integration with **LinkedIn**
- Better UX and descriptive homepage

### That's a wrap 🙏

Thanks a lot for reading. We would like to thank **[Linode](https://www.linode.com/)** and **[Hashnode](https://hashnode.com/)** for this amazing hackathon and for providing an amazing opportunity to build stuff.

**Special mention to [Peerlist](https://peerlist.io/) for providing us API access. 
**

-----------------------------------------------------------------------------------------------------------
Built by [Apoorv](https://twitter.com/apoorv_taneja) and Designed by [Naina](https://twitter.com/Naina_2728)









