# STC Tech Night #1 - Strapi

Welcome to STC Tech Night #1 🥳!

Here, we will learn about one of the most trending tool --- Strapi! Strapi is a flexible, open-source Headless CMS that gives developers the freedom to choose their favorite tools and frameworks while also allowing editors to easily manage and distribute their content.

Before we jump straight into the workshops, allow me to introduce ourself, do watch this short 1 minute video to know more 🎇!

[![intro video](/assets/banner.png)](https://www.youtube.com/watch?v=aBNvCoJP-ag)

Without further ado, let's get started!

## Table of content 📄

1. [Demo](#demo)

    1.1 [Installation](#installation)

    1.2 [API Endpoints](#apiendpoints)
    - [Types of content](#typesofcontent)
    - [Creating a new collection type](#collectiontype)
    - [New entry](#newentry)

    1.3 [Roles and permissions](#rolesandpermissions)

## Demo <a name="demo"></a>

A recorded session link will be inserted here after the event, if you prefer to watch the recorded session to follow the demo, feel free and go ahead! Otherwise, you may follow the step-by-step explaination below.

In this demo, we will be covering few features of Strapi 3.0:

1. [API Endpoints](#apiendpoints)
2. [Roles and permissions](#rolesandpermissions)

> Never have a lack of goals.
--- Lou Holtz

Let's start to learn by using an example, this is what we are going to have when we call the endpoint:

![goal](/assets/goal.png)

- One school can have many students

But before we jump into the topic, let's download and get strapi up and running!

<br>

### Installation <a name="installation"></a>

Because Strapi is written fully in javascript, hence it is necessary to have [nodejs](https://nodejs.org/en/) installed, go ahead and install if you haven't!

After you have your nodejs installed, open up your terminal and run:

```bash
npx create-strapi-app <YOUR PREFERRED FOLDER NAME> --quickstart
```

![install-1](/assets/install-1.jpg)

Hit enter and it should start creating a quickstart application.

> `--quickstart` use sqllite as default database, if you wish to have custom configuration, you can do it by overriding file in the future, or simply remove the --quickstart flag. see more at [https://strapi.io/documentation/v3.x/concepts/configurations.html](https://strapi.io/documentation/v3.x/concepts/configurations.html)

Grab your coffee and take a short break! Usually it will take a few while to download depending on your internet bandwidth, it's around few hundreds MB 😴.

You should see this once the strapi server is up and running

![install-2](/assets/install-2.jpg)

and an admin portal pop-up on your browser on `http://localhost:1337/admin`

![install-3](/assets/install-3.jpg)

Hurray! We had done our first module! 🎉

Just enter your favourite username and password (Don't use admin admin! 😜) and hit the "Ready to start" button!

----

### API Endpoints <a name="apiendpoints"></a>

We had done our installation and we are ready to create our first model!

But before that, let me explain what are the kind of model you can have in strapi...

<br>

#### Types of content <a name="typesofcontent"></a>

Now if you go and click on the `PLUGINS` -> `Content-Types Builder`, you can see there are 3 type of content you can create:

![api-1](/assets/api-1.jpg)

1. Collection type - Best for model `like user, restaurant, food, etc..`
2. Single type - Best for pages. `Like dashboard, home page, about us, etc...`
3. Component - Best for reusable model, `like Slots in the Schedule`, component **can't be** a standalone endpoint, it can only be attached to collection type and single type.

<br>

#### Creating a new collection type <a name="collectiontype"></a>

Click on the `PLUGINS` -> `Content-Types Builder` -> `COLLECTION TYPES` -> `Create new collection type`, and you should see a pop-up modal like this:

![api-2](/assets/api-2.jpg)

Type `School` and click `Continue`

Click on `Text` and enter `title`

![api-3](/assets/api-3.jpg)

Click `Finish`

Click `Save`

<br>

#### Adding new entry <a name="newentry"></a>

Now you had created your first model! Congrats 😁 You may continue and explore other kind of fields you can have in Strapi, but we will continue the flow for now

Let's go and create a school!

Click `COLLECTION TYPES` -> `Schools`

![api-4](/assets/api-4.jpg)

This is where you can see all the school entry, we haven't create any for now which is why it is empty.

Click on `Add new School` on your right.

Enter `Sunway Tech Club` on the `Title` field and hit `Save`!

You should now see an entry on your dashboard

![api-5](/assets/api-5.jpg)

You can now access the `School` model by going `http://localhost:1337/schools` (Do note it has an `s`)

All of the endpoints are created following [Open API Specification](https://swagger.io/specification/#:~:text=Introduction,or%20through%20network%20traffic%20inspection.)

You can take a look at Strapi documentation on the convention way of how the APIs are constructed [here](https://strapi.io/documentation/v3.x/content-api/api-endpoints.html#endpoints)

Now if we go to `http://localhost:1337/schools`, it's essentially open a `GET` request to get all entries of `School`.

Let's take a look on the endpoint...

![api-6](/assets/api-6.png)

Oops! What is this!! 😱 Did I do anything wrongly??

![api-7](/assets/api-7.jpg)
> source: [https://www.azquotes.com/quote/1486006](https://www.azquotes.com/quote/1486006)

Haha fret not! This is actually the expected behaviour, because:

> [you should receive a 403 error because you are not allowed, as Public user, to access to the articles.](https://strapi.io/documentation/3.0.0-beta.x/guides/auth-request.html#fetch-articles:~:text=you%20should%20receive%20a%20403%20error,user%2C%20to%20access%20to%20the%20articles.)

By default, Strapi will block all the request from anywhere unless you specify the permissions from the role.

In this case, we are accessing from `Public` role (Request without token, coming from nowhere).

----

### Roles and permissions <a name="rolesandpermissions"></a>