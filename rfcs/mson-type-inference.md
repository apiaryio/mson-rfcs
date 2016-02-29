---
RFC: XXXX
Author: Kyle Fuller
Status: Draft
Created: 2016-01-15
Last Modified: 2016-02-28
---

# MSON RFC XXXX: Type Inference

## Table of Contents

- [Abstract](#abstract)
- [Motivation](#motivation)
- [Rationale](#rationale)
- [Backwards Compatibility](#backwards-compatibility)

## Abstract

This proposal adds type inference to MSON, so that MSON parsers can determine
an appropriate type to use for each MSON member instead of defaulting to
`string`.

In short, the following example would result in a property called
`writable` which is of the type `boolean` and has a sample value of `true`.

```apib
+ writable: true
```

Previously, the above example would have resulted in a `string` with the
sample value `true`.

## Motivation

Type inference would simplify many uses of MSON and allow users to be less
explicit about the types. This makes the language more intuitive and simpler
for new users.

## Rationale

Below outlines the types of values that would be type-inferred.

### Boolean Types

The values `true` and `false` would automatically be treated as boolean values.

The following examples would be treated as boolean:

```apib
+ `is_admin`: true
+ `is_staff`: false
```

### Numeric Types

Positive and negative integers and decimal values will be treated as
"number" values.

The following examples would be treated as a number.

```apib
+ age: 32
+ amount: 99.99
+ balance: `-100`
+ x: `-0.0`
+ y: `-5.0`
```

## Backwards Compatibility

This RFC does propose breaking changes which can result in users types being
treated as different types that previously.

I believe that more often a user who used values that may be inferred as a
different type after this change originally intended that the type was as now
inferred.
