# My Awesome Blog

This is a Hexo blog using the Tranquility theme. It is automatically deployed to GitHub Pages using GitHub Actions.

## How to Use

### Create a New Post

To create a new post, run the following command:

```bash
hexo new "My New Post"
```

This will create a new Markdown file in the `source/_posts` directory. You can then edit this file to write your blog post.

### Run the Development Server

To preview your blog locally, run the following command:

```bash
hexo server
```

This will start a local server at `http://localhost:4000`.

### Deploy the Blog

The blog is automatically deployed to GitHub Pages whenever you push to the `main` branch. The deployment process is handled by the GitHub Actions workflow defined in `.github/workflows/deploy.yml`.

## Theme

This blog uses the [Tranquility](https://github.com/hooozen/hexo-theme-tranquility) theme.