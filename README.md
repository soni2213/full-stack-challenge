# Techstars Engineering: Fun Front to Back

Welcome to the Techstars Engineering Full Stack code Challenge. We work on diverse projects and value team members who can do it all from CSS to DevOps and everything inbetween.  We love to code and are passionate about doing it well.

This is your chance to show the team how you approach problems and give us insight into your abilities. For the challenge, you are required to design, develop, and style a Full Stack application using Rails or Node as the API and React as the front-end. Do not use Rails templates for your UI. Feel free to use any third party libraries you see fit. You will have **48 hours** to submit a solution for the given requirements.  If you need more time due to schedule conflicts, just let us know.  We value people with good communication skills. We strongly prefer that whatever you do, you do it well, as opposed to trying to razzle dazzle us.  Please read all the instructions carefully and email us if you have any questions.

## Getting Started
First, fork this repository into your own GitHub account. Then complete each of the parts below, working as you would in a professional environment. Once you have completed all the sections, please update the README, to reflect how to build and run your application, as well as any architectural decisions you have made. Add your deployment url to your github repo so we can test the deployed application. When you believe you are ready to submit your challenge, submit a pull request into our master branch. We will see the notification and get back to you on next steps.

## What we are looking for

* Ability to set up a REST API (Node or Rails preferred).
* Ability to set up a Relational Database
* Understanding of the HTTP protocol and how it works with REST API conventions
* Understanding the basics of CRUD
  * Create
  * Read
  * Update
  * Delete
* Ability to layout and design an HTML page with CSS
* Ability to create an intuitive UI using a front-end framework (React preferred)
* Ability to use Javascript on the front-end to interact with a REST API
* Ability to develop automated tests for your application
* Ability to translate user stories into a web application
* Ability to deploy a front-end and back-end stack.


## The Challenge

### Intro

Build an application that will be a directory of companies, and the people who have founded them. The main page should be a list of all the companies with some high-level information (Name, Short Description, City, State). When the user clicks on a company, show its details. Included in those details will be the founding members of company and a long description.

### Part 1 : Companies Index

1. Create the basic layout for the page
2. Create a list view of all companies
  * Company Name
  * Company Location
  * Short Description
3. Add ability to create a new company


![step 1](Step_1.png)

### Part 2 : Companies Create

1. Implement form to create a new company
2. Fields
    * Company Name __required__
    * Company Location (City, State) __required__
    * Company Description __required__
    * Founded Date


![step 2](Step_2.png)

### Part 3 : Company Details

1. Shows all of the Company's information
2. Ability to update Company
3. Ability to delete Company


![step 3](Step_3.png)

### Part 4 : Founders

1. In the Company details add the ability to add a Founder to a Company.
2. Each Founder can only belong to a single company.
3. Founder  Fields
    * Founder Full Name
    * Founder Title
4. Founders added should display in the company detail page.

![step 4](Step_4.png)

### Part 5 : Tests
Create a test suite for your application, writing unit and or functional tests that adequately cover the code base. TDD-ers will have already completed this challenge.

### Part 6 : Deployment
 Sign-up for a Heroku account (or other provider) and deploy your application to the web. Please provide us with the deployed URL. Bonus points for using a provider other than Heroku like AWS or Digital Ocean.  Please seed your application with at least a dozen Companies and Founders.

### Next Steps
If you move onto the next stage of the interview process we will have you come in and pair program with our engineers and build on top of your code base.  Example features we might implement together would be to add category tags, add a search component or add images to Companies and Founders using a third party hosting service.


# Documentation

#### Deployed at http://128.199.252.105/

The system is written using Ruby on Rails for APIs and ReactJS for frontend consumer.
Ruby version: 2.7.2
Ruby on Rails: 6.1.3
ReactJS version: 17.0.1
Postgresql: 12


# Backend
## Getting started
1. Clone the repo
2. ensure ruby 2.7.2, postgres 12 are installed
3. cd into the repo directory
4. run `bundle install`
5. run `bundle exec rails server`
6. to run specs `bundle exec rspec`

## Models
There are four total models:
1. Company
2. Founders
3. City
4. State

A company belongs to a city and can have many founders.
Founders have a unique email address.

All models have not null constraints, at both application as well as database level.
All foreign keys are indexed.

Whatever validations, and database hooks are there, have been put in the respective models. Controllers are lean and kept minimal.

All controller actions throw exception for anything unusual, which are caught in a basic *ExceptionHandler* Module.

APIs can be found [here](https://www.getpostman.com/collections/deb599077069b70f4ca0) (needs to be imported in Postman).

# Frontend
## Getting started
1. Clone the repo
2. ensure node is installed
3. cd into the repo directory
4. run `npm install`
5. run `npm start`

The frontend is built with ReactJS, and has been kept to bare minimum.
Have tried to keep the designs as consistent with the requirements as possible (Please excuse my css skills).

Have broken down components to small small chunks.
Primary components include:

1. CompanyList        -> Index page for all companies
2. AddCompany        -> Create new Company entry
3. UpdateCompany -> Update any existing company entry
4. CompanyDetails -> Show details of any individual company
5. FoundersList       -> Used in conjunction with CompanyDetails component, to show founders of the company
6. AddFounders      -> Partial form to add a new founder to the company.

# Deployment
Both backend and frontend applications are deployed on a linux (ubuntu) box.

Config:
2 GB RAM
50 GB Harddisk

### Backend
Below command will deploy the `master` branch onto the server.
`bundle exec cap staging deploy`

The database runs on the server itself, configuration is not exposed and can be found in the shared/config/database.yml file on the server.
Have used `capistrano` gem for deployment.

### Frontend
Frontend deployment is basic, as directed by create-react-app documentations.
Two steps are there:

1. `npm run build`
2. `scp -r ./build/* ubuntu@SERVER_IP:~/projects/web`
