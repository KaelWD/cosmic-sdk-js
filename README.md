<a href="https://beta.cosmicjs.com/signup">
  <img src="https://imgix.cosmicjs.com/ca74e2f0-c8e4-11ed-b01d-23d7b265c299-cosmic-dashboard-dark.png?w=2000&auto=format" alt="Cosmic dashboard darkmode" />
</a>

<h1 align="center">Cosmic JavaScript SDK</h1>

[Cosmic](https://www.cosmicjs.com/) is a [headless CMS](https://www.cosmicjs.com/headless-cms) (content management service) that provides a web dashboard to create content and an API toolkit to deliver content to any website or application. Nearly any type of content can be built using the dashboard then delivered using this SDK. [Get started free →](https://beta.cosmicjs.com/signup)

## Install

Install the Cosmic JavaScript SDK.

```bash
yarn add @cosmicjs/sdk
# OR
pnpm install @cosmicjs/sdk
# OR
npm install @cosmicjs/sdk
```

## Import

Import Cosmic into your app using the `createBucketClient` method.

```jsx
import { createBucketClient } from '@cosmicjs/sdk'
```

## Authentication

In the [Cosmic admin dashboard](https://beta.cosmicjs.com/login) go to _Bucket > Settings > API Access_ and get your Bucket slug and read key then set the variables in your app to connect to your Bucket.

```jsx
const cosmic = createBucketClient({
  bucketSlug: 'BUCKET_SLUG',
  readKey: 'BUCKET_READ_KEY'
})
```

## Get Objects

Objects are the basic building blocks of content in Cosmic.

### Get multiple Objects [[see docs](https://docs-v3.cosmicjs.com/docs/api/objects#get-objects)]

Use the `objects.find()` method to fetch Objects.

```jsx
const posts = await cosmic.objects.find({
  type: 'posts' 
})
.props([
  'title',
  'slug',
  'metadata'
])
.limit(10)
```

The above example fetches Objects in the `posts` Object type returning the `title`, `slug`, and `metadata` properties, limiting the response to `10` Objects.

### Get single Object by slug [[see docs](https://docs-v3.cosmicjs.com/docs/api/objects#get-a-single-object-by-slug)]

Use the `objects.findOne()` method with `type` and `slug` to fetch a single Object.

```jsx
const post = await cosmic.objects.findOne({
  type: 'pages',
  slug: 'home'
})
.props([
  'title',
  'slug',
  'metadata'
])
```

## Create, update, and delete Objects

To write to the Cosmic API, you will need to set the Bucket write key found in _Bucket > Settings > API Access_. (NOTE: never expose your write key in any client-side code)

```jsx
const cosmic = createBucketClient({
  bucketSlug: 'BUCKET_SLUG',
  readKey: 'BUCKET_READ_KEY',
  writeKey: 'BUCKET_WRITE_KEY'
})
```

### Create Object [[see docs](https://docs-v3.cosmicjs.com/docs/api/objects#create-an-object)]

Use the `objects.insertOne()` method to create an Object.

```jsx
await cosmic.objects.insertOne({
  title: 'Blog Post Title',
  type: 'posts',
  content: 'Here is the blog post content... still learning',
  metadata: {
    seo_description: 'This is the blog post SEO description.',
    featured_post: true,
    tags: ['javascript','cms']
  }
})
```

### Update Object [[see docs](https://docs-v3.cosmicjs.com/docs/api/objects#update-an-object)]

Use the `objects.updateOne()` method to update an Object by specifying the Object `id` and include properties that you want to update using `$set`.

```jsx
await cosmic.objects.updateOne({
  id: '5ff75368c2dfa81a91695cec'
},
{
  $set: {
    content: 'This is the updated blog post content... I got it now!',
    metadata: {
      featured_post: false
    }
  }
})
```

### Delete Object [[see docs](https://docs-v3.cosmicjs.com/docs/api/objects#delete-an-object)]

Use the `objects.deleteOne()` method to delete an Object by specifying the Object `id`.

```jsx
await cosmic.objects.deleteOne({
  id: '5ff75368c2dfa81a91695cec'
})
```

## Learn more

Go to the [Cosmic docs](https://docs-v3.cosmicjs.com) to learn more capabilities.

## Community support

For general help, please refer to [the official Cosmic documentation (v3)](https://docs-v3.cosmicjs.com). For additional help, you can use one of these channels to ask a question:

- [Slack](https://www.cosmicjs.com/community) (For live discussions with the Cosmic community and team)
- [GitHub](https://github.com/cosmicjs/cosmicjs/cosmic-sdk-js) (Bug reports, contributions)
- [Twitter](https://twitter.com/cosmicjs) (Get the latest news about Cosmic features and notifications)
- [YouTube](https://www.youtube.com/cosmicjs) (Learn from video tutorials)

## License

This project is published under the [MIT](https://github.com/cosmicjs/cosmic-sdk-js/blob/HEAD/LICENSE) license.
