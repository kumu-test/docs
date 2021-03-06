# Selectors

Selectors provide a simple way to select items within your project.
They're used everywhere in Kumu (perspectives, filter, focus, finder...
you get the point!) so you better cozy up to them.

You can build selectors by hand, or you can use our selector builder while you're
still getting comfortable with them (look for the rocket icon once you click on search)

![selector rocket](/images/selector-rocket.png)

You can always use general attribute selectors `[attribute=value]` but we've
built in a number of friendly shorthands to make selectors as easy to work
with as possible

We'll first run through the available shorthands, then we'll cover the general
attribute selector and the advanced queries you can create with them.

## Shorthand Selectors

### Slugs

Before we dive in, we need to talk about slugs. A slug is nothing more than
a simplified version of a value. To slug a value, simply:

1. Remove all special characters
2. Convert all spaces to a single dash
3. Lowercase everything

That's all there is to it! Here are some examples to clarify just in case the
idea is still a little hazy:

<table class="table">
  <tr><th>Original</th><th>Slug</th></tr>
  <tr><td>This is Kumu</td><td>this-is-kumu</td></tr>
  <tr><td>Honolulu, HI</td><td>honolulu-hi</td></tr>
  <tr><td>Friends don't let friends map alone!</td><td>friends-dont-let-friends-map-alone</td></tr>
  <tr><td>От Kumu с любовью</td><td>от-kumu-с-любовью</td>
</table>

Slugs are your friend! All shorthand selectors rely on slugs so make sure
your comfortable with them before moving on.

### By Collection

Selecting all of a given collection is pretty simple.

```
element     // select all elements
connection  // select all connections
loop        // select all loops
```

### By Type

Selecting all of a specific type is pretty simple too. (Noticing a pattern yet?)

For elements, just take the type and slug it. For connections, slug the type
and add "-connection".

```
person              // select all elements with "Person" element type
future-project      // select all elements with "Future Project" element type
personal-connection // select all connections with "Personal" connection type
business-connection // select all connections with "Business" connection type
```

### By Label

Selecting specific items by label is pretty simple too.
(Promise, that's the last one!)

Just slug the label and add a "#" to the front of it:

```
#jeff-mohr             // select element "Jeff Mohr"
#thinking-in-systems   // select element "Thinking in Systems"
#b1                    // select loop "B1"
```

### By ID

Sometimes you want to assign a friendly id so you don't need to use the
full label. Easy! Just assign your own "ID" attribute and now you can use that
to select items directly.

The syntax is the exact same as the label selector above.

```
#project-1234          // select item with id "project-1234"
```

### By Tag

To select by tag simply slug the tag and add a "." to the front of it:

```
.mission-critical  // select anything tagged with "Mission Critical"
```

## General Attribute Selector

While the shorthand selectors are great for most cases, they're only useful when
you just need to check for an exact value.  Attribute selectors are longer to
write but they're also much more powerful.

```
["element type"="person"] // select all elements with "Person" element type
["description"]           // select if description is present
["description"*="kumu"]   // select if description contains "kumu"
```

When working with numbers you can also use relative selectors:

```
[employees<20]
[employees>20]
[employees<=20]
[employees>=20]
```

Check out the [selector reference](/references/css-selector-reference.html)
for the full list of available operators.

## Complex Selectors

The selectors we've covered so far are just building blocks.  The real power
of selectors comes from being able to chain them together to create complex
queries.

Connect selectors back-to-back to AND them together (match all),
or join them with a comma to OR them (match any).

```
organization, person, project  // select all organizations, people, and projects
.young.influential[sex=female] // select all young influential women
```


Selectors provide a powerful, friendly way to slice through maps,
based on CSS selectors.

If you're familiar with css, you'll feel right at home.

## Universal Selector

```
*
```

The universal selector `*` matches all elements, connections, and loops.

## Type Selectors

```
General:  element, connection, loop
Specific: person, personal-connection
```

Type selectors come in two flavors: general and specific.

#### General

General type selectors match all items within the given collection. All projects
share the same three general type selectors: `element`, `connection`, and `loop`.

#### Specific

Specific type selectors are based on the assigned type. An element with
type "Person" would be selected using `person`. A connection with
type "Personal" would be selected using `personal-connection`
(just tack "-connection" onto the connection type).

## ID Selectors

```
Informal: #kumu, #honoluluhi
Assigned: #startup-29506
System:   #elem-123, #conn-123, #loop-123
```

ID selectors come in three flavors: informal, assigned, and system.

#### Informal

Informal ids are just the slugged version of the "label" attribute.
In most cases informal ids will be unique, permanent, and have the
added benefit of being naturally descriptive.

Because of their descriptive nature, we strongly recommend using informal ids whenever possible.

#### Assigned

If labels may change or simply aren't unique, you can assign your own
id to each object through the "id" attribute.  This gives you a unique
way to reference each object within your project however you please.

*Note: IDs must be strings and should be unique.*

#### System

System ids are automatically generated and assigned by Kumu.
They're guaranteed to be unique and permanent, making them an excellent
choice for permalink-style references.

All system ids are prefixed with the collection identifier, followed by
a unique random identifier.  For example: elem-123, conn-123, and loop-123.


## Tag Selectors

```
.influential
```

Tag selectors match all items tagged with the given value.
Make sure to keep your tags short and free from special characters to
avoid having to use a formal attribute selector (see below).

## Attribute Selectors

```
[tags~=influential]
```

Attribute selectors match all items with the given attribute condition.
Kumu supports a number of attribute operators to match against.

#### Presence

```
[description]
```

#### Absence

```
[!description]
```

#### Search

```
Starts with: [label ^= kumu]
Ends with: [label $= kumu]
Matches: [label *= kumu]
Includes: [skills ~= communication]
```

Note: the includes operator `~=` is only relevant for attributes with multiple values
(such as tags and skills).

#### Relative

```
[employees < 10]
[employees > 10]
[employees <= 10]
[employees >= 10]
```

<span class="edit-link"><a href="https://github.com/kumu/docs/blob/master/guides/selectors.md" target="_blank"><i class="fa fa-github"></i> edit this page</a></span>
