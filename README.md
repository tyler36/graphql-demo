# GraphQL with Laravel & View <!-- omit in toc -->

- [Intro](#intro)
- [Setup](#setup)
  - [GraphQL support](#graphql-support)

## Intro

- Based on [GraphQL with Laravel and Vue](https://laracasts.com/series/graphql-with-laravel-and-vue) series at Laracasts
- Auto-complete in testing is pretty handy: <kbd>shift</kbd> + <kbd>space</kbd>

## Setup

- Install Laravel

```shell
$ laravel new graphql-demo
$ php artisan --version
Laravel Framework 8.78.0
```

- Add a post model with related components

```shell
$ php artisan make:model Post -a
Model created successfully.
Factory created successfully.
Created Migration: 2022_01_05_000252_create_posts_table
Seeder created successfully.
Request created successfully.
Request created successfully.
Controller created successfully.
Policy created successfully.
```

- Add model relationships
- Add model seeder

### GraphQL support

- Install [Lighthouse](https://lighthouse-php.com/5/getting-started/installation.html)

```shell
# Install via composer
$ composer require nuwave/lighthouse
Publishing complete.

# Publish the default schema
$ php artisan vendor:publish --tag=lighthouse-schema
Publishing complete.

# Publish the default config
$ php artisan vendor:publish --tag=lighthouse-config
Publishing complete.

# Install devtools
$ composer require mll-lab/laravel-graphql-playground
Publishing complete.

# IDE Support helpers
$ php artisan lighthouse:ide-helper
```

- Update `graphql/schema.graphql` to include Posts and other relationships

```diff
type Query {
    users: [User!]! @paginate(defaultCount: 10)
    user(id: ID @eq): User @find
+    posts: [Post!]! @all
+    post(id: ID @eq): Post @find
}

type User {
    id: ID!
    name: String!
    email: String!
+    posts: [Post!]! @hasMany
    created_at: DateTime!
    updated_at: DateTime!
}

+ type Post {
+     id: ID!
+     title: String!
+     body: String!
+     user: User! @belongsTo
+     created_at: DateTime!
+     updated_at: DateTime!
+ }
```
