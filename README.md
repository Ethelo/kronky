# Kronky

Kronky bridges the gap between [Ecto](https://hexdocs.pm/ecto/Ecto.html) and [Absinthe GraphQL](http://absinthe-graphql.org/) with formatted validation messages in a mutation payload.

The primary philosophy is that invalid and/or unexpected user input is DATA, and should be returned as such.
On the other hand, errors made in using an api - like querying a field that doesn't exist, are actually ERRORS and should be returned as errors.

I recommend reading [Validation and User Errors in GraphQL Mutations](https://medium.com/@tarkus/validation-and-user-errors-in-graphql-mutations-39ca79cd00bf) for more discussion on this. The excellent people behind Absinthe also approve this style from what I've seen in their slack.

## Installation

Kronky will be available on Hex soon! Once
 [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `kronky` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [{:kronky, "~> 0.1.0"}]
end
```

## Usage

The best place to find usage examples is by looking at the test cases at the [Kronky Github](https://github.com/Ethelo/kronky) or the docs for `Kronky.Payload`


Here's a quick summary of what Kronky includes

`Kronky.ValidationMessage` structs/objects are created with all the information you'd normally be able to access through [Ecto.Changeset.traverse_errors/2](https://hexdocs.pm/ecto/Ecto.Changeset.html#traverse_errors/2).

Kronky includes a schema definition to add ValidationMessages to your schema.

Kronky.Payload is middleware that takes your resolver output (either an updated object or a changeset with errors) and converts into a Kronky Mutation Response (aka Payload).

Payloads have three fields

- `successful` - Indicates if the mutation completed successfully or not. Boolean.
- `messages` - a list of validation errors. Always empty on success
- `result` - the data object that was created/updated/deleted on success. Always nil when unsuccesful

Finally Kronky.TestHelper has some helper methods that make it easier to write Exunit tests against your schema.

## Caveats

Kronky **does not** currently support nested changesets/graphql objects. It'll probably die horribly if you try. If you need this feature, Kronky may not be for you.

Kronky is very very tightly coupled to Ecto internals, which is probably not a good thing.
Any change in how Ecto.Changeset stores/returns validation errors will likely break Kronky until I can update. Use with caution!

## Roadmap

 - Handle Nested Changesets/Objects
 - investigate identifying validations through `Changeset.validations` instead of matching on specific error texts.

If you find any issues, or have suggestions for improvements, please open an issue.

## Ethelo

Kronky is maintained and funded by [Ethelo](http://ethelo.com/). Ethelo focuses collective wisdom to find smart, practical and well-supported solutions to tough challenges. Learn about our corporate offerings at http://ethelo.com/, and our social change efforts at http://ethelo.org/.

## Why Kronky?

![Kronk transling Squirrel](https://ci.memecdn.com/1254392.gif)
