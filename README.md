# Build a Blog with Dynamic Routing and Client-Side Fetching
## Objective
Build a small blog using Nuxt.js where posts are fetched from a static JSON file (or mocked API), and each post is viewable on a dynamic route. You will also implement basic client-side interactivity and apply a simple CSS framework like TailwindCSS or Vuetify for UI design.

# Requirements
## Project Setup
Use Nuxt.js (v3) to create the project.
Set up a basic layout with a header and footer using a CSS framework like TailwindCSS or Vuetify.

## Home Page
Display a list of blog posts on the homepage (use a static JSON file or hardcoded data as your mock "API").
Each post should display the title, a short excerpt (e.g., first 100 characters), and a "Read More" button.
When a user clicks "Read More," they should be taken to the individual post page.

## Dynamic Post Pages
Use dynamic routing to create a page for each individual post (e.g., /posts/_slug.vue).
The post page should display the full content of the post.

## Client-Side Fetching
Fetch data on the client-side using useFetch or fetch within Nuxt.js, either from a local JSON file or a mocked API.
Ensure that the data fetching is handled asynchronously (show loading indicators or a placeholder while data is being fetched).

## Styling and UI
Use TailwindCSS or Vuetify to style the layout.
Add basic UI elements like a responsive navigation bar, a footer, and a loading spinner or skeleton loader for when data is being fetched.

The general design and aesthetics are up to you, so feel free to come up with a simple, modern and responsive design.

# Bonus Features (if time allows):
Implement a simple search bar that filters posts by title or content.
Implement multi-language support.
Integrate Google Analytics.
Add pagination or infinite scrolling on the home page.
Implement basic form validation for a "Contact" form (could be a simple static form without actual submission functionality).

