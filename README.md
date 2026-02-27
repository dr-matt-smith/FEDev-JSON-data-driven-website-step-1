Back to FEDev main <<<< https://github.com/dr-matt-smith/2026-FDEev-Front-End-Dev-start-here

JSON-driven website: 
Step 1
|
[Step 2](https://github.com/dr-matt-smith/FEDev-JSON-data-driven-website-step-2)
|
[Step 3](https://github.com/dr-matt-smith/FEDev-JSON-data-driven-website-step-3)
|
[Step 4](https://github.com/dr-matt-smith/FEDev-JSON-data-driven-website-step-4)
|
[Step 5](https://github.com/dr-matt-smith/FEDev-JSON-data-driven-website-step-5)
|
[Step 6](https://github.com/dr-matt-smith/FEDev-JSON-data-driven-website-step-6)
|
[Step 7](https://github.com/dr-matt-smith/FEDev-JSON-data-driven-website-step-7)

# FEDev-JSON-data-driven-website-step-1

Step-by-step development of a module details website. Routing in the form `/module/H2037`


What is a "slug"
- https://yoast.com/slug/
- a user-friendly ID
- objects from DB have a natural ID
- things like blog posts can have slug IDs created by connecting words with hypens, 
  - e.g. "`university-hands-out-free-ice-cream`"

for this project we'll refer to unique module code number IDs
- such as `/modules/2037`
- but often you'll see a generic `/routes/blog/[slug]/+page.svelte` pattern ...

## 0: create a new SvelteKit project
Create a new Sveltekit project the usual way
- `npx sv create`
- Sveltkit minimal
- JavaScript with JSDoc
- npm package management


## 1: create home page `/routes/+page.svelte`

![all module routes get same placholder messsage](/screenshots/1_module_links.png)


Make the website home page `/routes/+page.svelte` provide links to 3 modules:
- H2037 Front End Dev
- H2019 Database Fundamentals
- H2031 Object-Oriented Programming

We'll use the "H" code numbers as the IDs/slugs:
- `/modules/2027`
- `/modules/2029`
- `/modules/2031`

here's the code for the simple home page: `/routes/+page.svelte`
```html
<h1>MGW - my great website</h1>

<p>learn more about:</p>

<ul>
    <li>Degree programmes (coming soon)</li>
    <li>Evening classes (coming soon)</li>
    <li><a href="/modules">modules</a></li>
</ul>
```

## 2: a modules list page with links to 3 modules `/routes/modules/+page.svelte`

Create folder `/routes/modules`

here's the code for the modules list page `/routes/modules/+page.svelte`
```html
<h1>Welcome to Modulesite</h1>

Learn more about year 2 modules
<ul>
    <li>
        <a href="/modules/2027">H2037 Front End Dev</a>
    </li>
    <li>
        <a href="/modules/2029">H2029 Database Fundamentals</a>
    </li>
    <li>
        <a href="/modules/2031">H2031 Object-Oriented Programming</a>
    </li>
</ul>
```

## 3: create our placeholder module details page `/routes/modules/[modulecode]/+page.svelte`

![module details coming soon](/screenshots/3_module_coming_soon.png)

Create folder `/routes/modules/[modulecode]` 
- yes include the square brackets `[` and `]` in directory name!
- this is how Sveltekit routing identifies a parameterisesd URL

Create file `/routes/modules/[modulecode]/+page.svelte` containing a coming-soon message:
```html
<p>
    module coming soon
    <br>
    <a href="/">
        &lt;-  back to home page
    </a>
</p>
```

Now, regardless of the value in the HTTP Request URL after `/modules/` the user will see the same placeholder page content.

## 4: add nav bar links into site layout for all pages `/routes/+layout.svelte`

Let's add a little bit of a nav bar for the top of each page. We'll add a link to the homage page and to the modules list page:
- `home | modules`

Code in `/routes/+layout.svelte` will be for all pages in the website.
- the content of individual pages is delivereyed by `{@render children()}` in template files

```html
<script>
  import favicon from '$lib/assets/favicon.svg';

  let { children } = $props();
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
</svelte:head>

<nav>
  <a href="/">home</a>
  |
  <a href="/modules">module list</a>
</nav>
<hr>

{@render children()}
```
