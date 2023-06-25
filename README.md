# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Issue: Add a new toy when the toy form is submitted

- Checked the terminal logs.
- Added a `byebug` at the start of the `create` action in the `ToysController`.
- Inspected the code and variables in the debugger to identify the problem.
- Noticed a typo in calling the `Toy` model, which was causing an error.
- Fixed the typo by changing `Toys.create` to `Toy.create`.
- Tested the toy form submission again, and it worked successfully.

- Issue: Update the number of likes for a toy

- Checked the terminal logs.
- Added a `byebug` at the start of the `update` action in the `ToysController`.
- Inspected the code and variables in the debugger to identify the problem.
- Found that the `id` parameter was not permitted in the `toy_params` method.
- Modified the `toy_params` method to include `:id` in the permitted parameters.
- Added `render json: toy, status: :ok` after the `toy.update(toy_params)` line to return the updated toy in the response.
- Tested updating the number of likes for a toy, and it was successfully updated.

- Issue: Donate a toy to Goodwill (and delete it from our database)

- Examined the error message in the terminal logs.
- Found that there was no `destroy` route defined to handle the toy deletion.
- Added the `destroy` action in the `ToysController`.
- In the `destroy` action, located the toy using `Toy.find_by(id: params[:id])`.
- Called the `destroy` method on the toy to remove it from the database.
- Set the response status to `:no_content` using `head :no_content`.
- Tested deleting a toy, and it was successfully deleted from the database.
