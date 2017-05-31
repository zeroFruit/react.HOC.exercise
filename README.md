# Connect And Provider

### How they communicate?

__[Provider > Redux Store] <=> [Connect > Component]__

__Redux Store__: Redux actual lib. It is object which holds global app state that is formed by every reducers. Provider watches changes of Redux Store. And Provider broadcast every connected child component

Connect is HOC which is directly communicate with Provider



### All of these are HOC

HOC is adding additional functionality or data to React Component 



# React-Router

```react
import { Router, Route, browserHistory } from 'react-router';
```

* ```Router``` is top level object, watch the URL 
* ```browserHistory``` keep track of ```Router``` 's URL





Component itself has no idea of authentication. HOC job is implement this kind of shared logic which is reusable of many diff Components.



# HOC

HOC is calling existing Component. HOC exporting function that receives React Component then return different class Component



Resources Component wrapped with Auth HOC (Render Resources + maybe add on some additional behavior ). Let's call this wrapped Resources Component as Wrapped Resouces.

At some time later, we want to add new props to original Resources Component by just adding new props into Wrapped Resources.

```react
import React, { Component } from 'react';

export default function(ComposedComponent) {
  class Authentication extends Component {
    render() {
      return <ComposedComponent { ...this.props }/>
    }
  }

  return Authentication;
}

```

```react
// in other modules
import Authentication // This is my HOC
import Resouces // This is the component I want to wrap

const ComposedComponent = Authentication(Resources);

// In some render method...
<ComposedComponent resources={resourceList} /> // resouces is passed into this.props
```



# React Router Context

__Router => App => AuthenticationHOC(Resources)__

* Need access to the router to programatically navigate the user. The router is some parent component - use 'context' to get a reference.
* context is simliar to props but it spans all around the Component tree so it can navigate from child Component to parents



React forcebly us to prevent to abuse this context by forcing us to define ```contextTypes``` property.

So if we want to use ```router``` property, should predefine the types of ```router``` 

```react
static contextTypes = {
  router: React.PropTypes.object
}
```

