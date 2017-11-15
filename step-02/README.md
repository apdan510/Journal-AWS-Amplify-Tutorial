# Step 02 - Authentication

AWS Amplify solved the authentication for developers. Let's use it.

## 1. Prepare

Install package, core library and react specific.
```
npm install --save aws-amplify
npm install --save aws-amplify-react
```

**Create a AWS Mobile Hub project**

Go to [Mobile Hub Import](../mobile-hub-import) to quickly setup the backend on AWS.

**Download config file**

Once project created, open "Hosting and Streaming"
![Hosting and Streaming](host_and_streaming.png)

At the bottom of page, "Download aws-exports.js file".
![Download aws-exports.js file](download_aws_exports.png)

Download and save to `src` folder

## 2. Configure AWS Amplify

Open `src/App.js`, add these lines
```
import Amplify from 'aws-amplify';
import aws_exports from './aws-exports';

Amplify.configure(aws_exports);
```

## 3. Add Authenticator

Open `src/modules/Login.jsx`, change content to:
```
import React, { Component } from 'react';

import { Authenticator } from 'aws-amplify-react';

export default class Login extends Component {
    render() {
        return <Authenticator />
    }
}
```

Now `npm start`. Login becomes real
![Authenticator](authenticator.png)
Got ahead sign up and sign in. Create a test user.

## 4. Greetings

Notice after sign in, there is a sign out button. It makes sense to have sign out button. However in our case the place is not right.

**Hide Greetings**

Let's hide this one. `src/modules/Login.jsx` becomes:
```
import React, { Component } from 'react';

import { Authenticator, Greetings } from 'aws-amplify-react';

export default class Login extends Component {
    render() {
        return <Authenticator hide={[Greetings]} />
    }
}
```

`Authenticator` is composed of a group of pieces, `Greetings` is one of them. `hide` defines a list of pieces to be hidden. Try put `SignIn` in list.

**Greetings on Menu**

What we actually want. Is the greetings on Menu, top-right corner. So we want to edit where the Menu is, `App.js`.

First import Greetings
```
import { Greetings } from 'aws-amplify-react';
```

The default styling doesn't fit in our UI, lets add the menu item and remove default theme of Greetings.
```
const GreetingsTheme = {
    navBar: {
    },
    navRight: {
    }
}

...

    <Menu.Menu position="right">
        <Menu.Item>
            <Greetings theme={GreetingsTheme} />
        </Menu.Item>
    </Menu.Menu>
```