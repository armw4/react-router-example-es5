# react router example es5 for Julia G :fire:

This demos using react-router without node.js and an additional transpile step at build time. I've extracted
the boilerplate template from the react tutorial page and drafted a very contrived example of how to accomplish
this without the learning curve of node. react-router's examples are all in ES6, and it's not obvious how to get
started with plain old JavaScript. How does this work?

#### 1. Load babel locally or via CDN

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
```

#### 2. Create your JSX/JavaScript content via type="text/babel"

```
<body>
  <div id="content"></div>
  <script type="text/babel" src="scripts/example.js"></script>
  <script type="text/babel">
    // To get started with this tutorial running your own code, simply remove
    // the script tag loading scripts/example.js and start writing code here.
  </script>
</body>
```

#### 3. You have the right to JSX

Now babel will compile your code to vanilla JS for you all within the context of the browser. No server step is necessary here.
Why would you want to do this? If you're not familiar with node and don't have the desire or time to set it up, you'll want to bypass `npm`, etc.
and get something cooked up really fast.

The server in this repository still leverages node to serve the index page, but this was purely optional. You could open `public/index.html` directly
in your browser and the code should still work.

#### Running the node server

```sh
git clone https://github.com/armw4/react-router-example-es5.git
cd react-router-example-es5
npm install
npm start &
open http://localhost:3000
```

Now start clicking around on the links and watch the SPA do it's thing.

#### The server wildcard/catch all route is a thing

If you decided to server your app from an actual web server, you'll need a catch all route
for the purposes of deep linking. For example, I shouldn't have to hit the index route in order to access the app.
It should load an arbitrary, route, so long as it's valid and the user can access it, no matter how the user gets
to that route (i.e. I could manually type the route in my address bar, or click a link from an email). This is pretty
simple to configure in node as I've done in `app.js`. You'll want to do the same in the framework of your choosing.
This works because the browser will always download a copy of your app from the server, *then* trigger any client side
route handlers you have configured (and in that order :wink:).

#### Where's the magic happening?

The app itself lives inside `public/index.html`. It's here that react, history, react-router, etc. is initialized. Our components and routing configuration
live here as well.

#### What's the {this.props.children} thing?

react-router will provide the component attached to any sub routes via `this.props.children`. It simply adds them to the DOM under their parent (at an arbitrary
depth of course). Without calling `{this.props.children}` from the parent routes, we'd never see the content of any child components. Keep this in mind when
building nested routes.

#### Why is history required?

TL:DR history gives us pretty urls. Without it, we'd have to target urls with the `#` in them. So you'd see `<Link to="#details">Details</Link>` instead of
`<Link to=/"details">Details</Link>`. react-router itself also leverages history under the hood.

#### Cheers, and happy reacting

:wink:
