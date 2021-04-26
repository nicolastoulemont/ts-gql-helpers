# ts-gql-helpers

ts-gql-helpers is a set of helpers functions aiming to improve the DX of GraphQL and Typescript projects.

## Installation

```bash
npm i ts-gql-helpers
or
yarn add ts-gql-helpers
```

## Functions

### Unions helpers

- isType()

```typescript
interface Object extends {
  name: 'object',
  __typename:  'Object'
}
interface OtherObject extends {
  title: 'other object',
  __typename: 'OtherObject'
}

isType(object,'Object'):boolean

// Usage
// type object = Object | OtherObject
if(isType(object,'Object')) {
  // object.name will be infered as valid
}

```

- isTypeInTuple()

```typescript
interface Object extends {
  name: 'object',
  __typename: 'Object'
}
interface OtherObject extends {
  title: 'other object',
  __typename: 'OtherObject'
}
// typeof Tuple = Array<Object | OtherObject>
const typedArrayOfObject = tuple.filter(isTypeInTuple('Object'))
const typedArrayfOtherObject = tuple.filter(isTypeInTuple('OtherObject'))

// Possible undefined
tuple[0].name
tuple[0].title

// Infered as valid
typedArrayOfObject[0].name

// Infered as valid
typedArrayfOtherObject[0].title
```

- isEither()

```typescript
interface Object extends {
    name: 'object',
  __typename: 'Object'
}
interface OtherObject extends {
   name: 'other object',
  __typename: 'OtherObject'
}
interface AnOtherObject extends {
   title: 'another object',
  __typename: 'AnOtherObject'
}
// typeof object = Object | OtherObject | AnOtherObject
isEither(object, ['Object', 'OtherObject']):boolean

// Usage
if(isEither(object, ['Object', 'OtherObject'])) {
  // object.name will be infered as valid
  // object.tile will be infered as undefined
}
```

- isNot()

```typescript
interface Object extends {
    name: 'object',
  __typename: 'Object'
}
interface OtherObject extends {
   name: 'other object',
  __typename: 'OtherObject'
}
interface AnOtherObject extends {
   title: 'another object',
  __typename: 'AnOtherObject'
}
// typeof object = Object | OtherObject | AnOtherObject
isNot(object, ['Object', 'OtherObject']):boolean
// Usage
if(isNot(object, ['Object', 'OtherObject'])) {
  // object.name will be infered as undefined
  // object.tile will be infered as valid
}
```
