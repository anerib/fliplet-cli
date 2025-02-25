# Building components

To start creating a component, use the CLI to generate a boilerplate including the basic things you'll need:

```
$ fliplet create-widget "my-awesome-component"
```

The above code will create a new folder named "my-awesome-component" including the skeleton of your component, including these files:

```
css/
img/
js/interface.js
widget.json
interface.html
build.html
```

To run your component, simply navigate to its folder and use the `run` command:

```
cd my-awesome-component
fliplet run
```

The above command will run the development server at [http://localhost:3000](http://localhost:3000). The local development server uses sample data to speed up your development, so you don't have to worry about creating apps, screens, data etc.

While the development server is running, any changes made to Handlebars `.hbs` template files will compiled so that templates access from `Fliplet.Widget.Templates()` are up to date.

We'll first focus on the `widget.json`, which is the definition of your component. If you're used to npm, it's similar to the `package.json` file for npm modules.

## Creating a component interface using the advanced Vue.js boilerplate

If you're building a component interface and want to use the advanced Vue.js-based boilerplate, simply use the `--vue` option as described below.

<p class="warning"><strong>Version 5.1.0 required:</strong> Please note that this feature does require the version 5.1.0 or newer of the Fliplet CLI.</p>

```
$ fliplet create-widget "my-awesome-component" --vue
```

Once done, follow the instructions in the `README.md` file in the generated folder to get started.

## Including external libraries

Components should never include script/link tags to reference external assets (like **vendor libraries**), but rather define them as `assets` via the `widget.json` file. Check the section below for more details.

## The component definition file

The `widget.json` file defines your component as well as the **dependencies** and **assets** it needs in order to run.

```json
{
  "name": "my Awesome Component",
  "package": "com.example.my-awesome-component",
  "dependencies": [],
  "assets": []
}
```

Please note: if you make changes to the `widget.json` file, restart the development server (`fliplet run`) to apply the changes you made.

[Read more about the widget.json](components/Definition.md)
{: .buttons}

---

## Instances

Once a component is dropped onto a page (or an app component is added as an add-on), an instance of such component will be created in the system for the app.

A component instance (internally called `Widget Instance`) can save settings for the instance of the component.

Components can save their settings through our JS APIs (available via the `fliplet-core` package):

```js
Fliplet.Widget.save({
  someValue: true,
  otherValue: 1,
  supportsObjects: {
    a: 'Hello',
    b: 'World'
  }
});
```

As you can see, plain Javascript objects (which can be serialized to JSON) are supported.

---

## UI: Interface and Output (build)

**All components** can define a **html interface** where their settings for the instance can be configured. An interface is made of a HTML page (which is compiled via Handlebars from the engine) and any number of assets (JS, CSS, etc).

In addition, **app and page components** should also define a **html output** (internally called `build`) to be displayed in the page when they are dropped in.

Therefore, to recap:

- [interface.html](components/Interface) defines the interface for app components, page components and providers
- [build.html](components/Build-output) defines the output of an app or page component

### Sample interface.html

{% raw %}
```handlebars
<form>
  <input type="text" name="videoUrl" value="{{ videoUrl }}" placeholder="A video url" />
</form>
```
{% endraw %}

[Jump to the interface documentation](components/Interface.md)
{: .buttons}

---

### Sample build.html

{% raw %}
```handlebars
{{#if videoUrl}}
  <video src="{{ videoUrl }}"></video>
{{/if}}
```
{% endraw %}

[Jump to the build (output) documentation](components/Build-output.md)
{: .buttons}

---

