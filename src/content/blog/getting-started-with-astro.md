---
title: "Getting Started with Astro"
date: "August 15, 2025"
---

Astro is an amazing framework for building fast websites. In this post, I share my experience getting started with Astro and how it compares to other frameworks.

## Why Astro?

Astro is a modern framework designed for building content-focused websites. It allows you to use your favorite UI components (React, Vue, Svelte, etc.) but delivers zero JavaScript by default, resulting in extremely fast loading times.

## Key Features

- **Component Islands:** Use UI framework components but only hydrate them when necessary
- **Zero JavaScript by default:** Send only HTML and CSS to the browser
- **Edge-ready:** Deploy anywhere with ease
- **Customizable:** Tailwind, MDX, and hundreds of integrations to choose from

## Getting Started

Starting a new Astro project is simple. You can use the following command:

```bash
npm create astro@latest
```

This will guide you through the setup process and create a new Astro project with the default template.

## Creating Your First Component

One of the best things about Astro is how intuitive it is to create components. In fact, the card components you see on this blog's home page are built using an Astro component! 

Here's the code for the Card component that's being used throughout this site:

```astro
---
// src/components/Card.astro
// This is the component script section (uses frontmatter syntax)

// Define the props that the component accepts
interface Props {
  title: string;
  body: string;
  href?: string;
  imgSrc?: string;
}

// Destructure the props with defaults
const { 
  title, 
  body, 
  href = '#',
  imgSrc 
} = Astro.props;
---

<!-- This is the component template section -->
<div class="card">
  {imgSrc && <img src={imgSrc} alt={title} class="card-image" />}
  <div class="card-content">
    <h2 class="card-title">{title}</h2>
    <p class="card-body">{body}</p>
    <a href={href} class="card-link">Read more</a>
  </div>
</div>

<style>
  /* This CSS is scoped to this component only */
  .card {
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
    background-color: white;
  }
  
  .card:hover {
    transform: translateY(-5px);
  }
  
  .card-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }
  
  .card-content {
    padding: 1.5rem;
  }
  
  .card-title {
    margin-top: 0;
    margin-bottom: 0.5rem;
    font-size: 1.5rem;
    color: #333;
  }
  
  .card-body {
    margin-bottom: 1.5rem;
    color: #666;
    line-height: 1.6;
  }
  
  .card-link {
    display: inline-block;
    color: #0066cc;
    text-decoration: none;
    font-weight: 500;
  }
  
  .card-link:hover {
    text-decoration: underline;
  }
</style>
```

You can then use this component in any of your pages:

```astro
---
// src/pages/blog.astro
import Layout from '../layouts/Layout.astro';
import Card from '../components/Card.astro';
import { getCollection } from 'astro:content';

const blogPosts = await getCollection('blog');
---

<Layout>
  <main>
    <h1>My Blog</h1>
    
    <div class="blog-posts">
      {blogPosts.map(post => (
        <Card
          title={post.data.title}
          body={post.body.split('\n\n')[0]}
          href={`/blog/${post.slug}`}
        />
      ))}
    </div>
  </main>
</Layout>
```

This demonstrates Astro's component model, which combines HTML, CSS, and JavaScript in a single file, similar to other modern frameworks but with the benefit of shipping zero JavaScript by default.

## Conclusion

Astro has been a game-changer for my web development workflow. The ability to use components from any UI framework while still delivering lightning-fast websites is unmatched. I highly recommend giving it a try for your next project!