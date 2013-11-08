# Resource Blueprint
A proposal of resource-oriented, protocol-independent [API Blueprint](http://apiblueprint.org). This proposal is focused on modeling API resources, its attributes, affordances and an API state machine.

## Use Case API
As an use-case API the Resource Blueprint uses [Gist Fox API](../examples/Gist%20Fox%20API.md). To demonstrate the description of the API state machine the Gist Fox API is extended with additional resource states.

The actual proposal source can be found in the [Gist API.md](Gist%20API.md) file. Refer to [Resrouce Blueprint Syntax](#syntax) for 

## Gist State Machine

### Gists Resource 
An entry point to Resource Blueprint Gist API is the `Gists` resource in its `collection` state. This resource has two states: `collection` and 
`navigation`:

![fig1](assets/Gist%20State%20Machine%20001.png)

> **Note:** Collection essentially servers as a factory for individual entities.

### Gist Resource
The `Gist` resource, created by the `create` affordance of the `Gists` Resource has following two states: `active` and `archived` each with appropriate set of affordances:

![fig2](assets/Gist%20State%20Machine%20002.png)

### Embedded Entities
Finally a `Gist` resource embedded in the `Gists` resource can be accessed via the `self` affordance of the particular embedded entity forming the complete API state machine:

![fig3](assets/Gist%20State%20Machine%20003.png)

<a name="syntax"></a>
## Resource Blueprint Syntax

### Keywords
New keywords introduced in the Resource Blueprint are:

+ `API Entry Point` - denotes state machine entry point referencing a resource and its state
+ `Resource` - definition of a resource e.g. `Resource <resource name>`
+ `Attributes` - definition of resource attributes. Alt keyword: `Properites`
+ `Affordances` - definition of **all** resource's affordances. Alt keywords: `Transition`, `Actions`, `Link Relations`
+ `States` - definition of resource states and state transitions invoked using affordances.

	Each state should lists all available affordances the final state of using the relevant affordance in format:

	```
	<affordance> -> <new state>
	```

	The new state might be a reference to another resource state (see Referencing Syntax bellow). One affordance per state should be marked as `self` to represent the default "retrieve" affordance. 

+ `Conditions` - list of conditions for an affordance to be available in the respective state. Alt keywords: `Permissions`, `Rights`

> **Note:** Consider using Alt keywords to improve clarity for majority of users.

### Referencing Syntax
+ Reference to the resource default state: `[<resource>][]`
+ Reference to a resource state: `[<resource>#<state>][]`
+ Reference to a resource affordance: `[<resource>.<affordance>][]`


> **Note:** Conditions, Permissions, Rights is associated with business rules tied to an affordance being available or present in a response.