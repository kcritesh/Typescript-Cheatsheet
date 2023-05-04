# Typescript-Cheatsheet
TS Cheatsheet. (Open For Contribution)

TypeScript cheat sheet for use with Next.js:

### TypeScript Configuration

To use TypeScript with Next.js, you need to add a `tsconfig.json` file to the root of your project with the following configuration:

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "lib": ["dom", "dom.iterable", "esnext"],
    "esModuleInterop": true,
    "allowJs": true,
    "sourceMap": true,
    "jsx": "preserve",
    "moduleResolution": "node",
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "exclude": ["node_modules", ".next"]
}
```

This configuration specifies the TypeScript version, target, and module system. It also includes the necessary libraries for Next.js and sets up paths for module resolution.

### Next.js Configuration

To use TypeScript with Next.js, you also need to update your `next.config.js` file with the following configuration:

```javascript
module.exports = {
  webpack(config) {
    config.resolve.alias['@'] = path.resolve(__dirname, 'src')
    return config
  }
}
```

This sets up an alias for module resolution so you can use the `@` symbol to import files from your `src` directory.

### React Components

To create a TypeScript-based React component in Next.js, you can use the following syntax:

```typescript
import React, { FC } from 'react'

interface Props {
  name: string
}

const MyComponent: FC<Props> = ({ name }) => {
  return (
    <div>
      Hello, {name}!
    </div>
  )
}

export default MyComponent
```

This code defines a component that takes a `name` prop of type `string`. The `FC` type is a shorthand for `FunctionComponent`, which is a generic type that takes a prop interface as a parameter.

### Static Props and Paths

To use TypeScript with static props and paths in Next.js, you can use the following syntax:

```typescript
import { GetStaticProps } from 'next'

interface Props {
  name: string
}

const HomePage = ({ name }: Props) => {
  return (
    <div>
      Hello, {name}!
    </div>
  )
}

export const getStaticProps: GetStaticProps<Props> = async () => {
  const name = 'World'

  return {
    props: {
      name
    }
  }
}

export default HomePage
```

This code defines a Next.js page component that takes a `name` prop of type `string`. The `GetStaticProps` type is a generic type that takes a prop interface as a parameter.

### Dynamic Routing

To use TypeScript with dynamic routing in Next.js, you can use the following syntax:

```typescript
import { GetStaticPaths, GetStaticProps } from 'next'

interface Props {
  id: string
}

const PostPage = ({ id }: Props) => {
  return (
    <div>
      Post {id}
    </div>
  )
}

export const getStaticPaths: GetStaticPaths = async () => {
  const paths = [{ params: { id: '1' }}, { params: { id: '2' }}]

  return {
    paths,
    fallback: false
  }
}

export const getStaticProps: GetStaticProps<Props> = async ({ params }) => {
  const id = params?.id

  return {
    props: {
      id
    }
  }
}

export default PostPage
```

This code defines a dynamic page component that takes an `id` parameter as a prop. The `GetStaticPaths` type is used to specify the possible dynamic routes for the component, while the `GetStaticProps` type is used to fetch data for the component.

In this example, the `getStaticPaths` function returns an array of possible `id` values for the component, while the `getStaticProps` function fetches data for the selected `id`.

### Conclusion

TypeScript can be a powerful tool for developing Next.js applications, as it provides static typing and improves code reliability. By using the above configurations and syntax, you can easily integrate TypeScript into your Next.js project and create type-safe components, pages, and routes.
