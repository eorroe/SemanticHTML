# SemanticWEB

This is a proposal for a **real Semantic WEB** using the `is` attribute in our `HTML/DOM`:

This is how we currently write some `HTML`:

```HTML
<div id="steps">
  <div class="step">
    <h1 class="stepTitle"></h1>
    <span class="stepInfo"></span>
    <button class="stepAction"></button>
  </div>
  <div class="step">
    <h1 class="stepTitle"></h1>
    <span class="stepInfo"></span>
    <button class="stepAction"></button>
  </div>
  <div class="step">
    <h1 class="stepTitle"></h1>
    <span class="stepInfo"></span>
    <button class="stepAction"></button>
  </div>
</div>
```

What if we could write our markup like this:

**First think you'll notice is I'm using `app` keyword, this is just what I would use but corresoponding to the app. For a Twitter application I may use `twitter`**

```HTML
<app-steps>
  <app-step>
    <app-step-title is="h1"></app-step-title>
    <app-step-info is="span"></app-step-info>
    <app-step-action is="button"></app-step-action>
  </app-step>
  <app-step>
    <app-step-title is="h1"></app-step-title>
    <app-step-info is="span"></app-step-info>
    <app-step-action is="button"></app-step-action>
  </app-step>
  <app-step>
    <app-step-title is="h1"></app-step-title>
    <app-step-info is="span"></app-step-info>
    <app-step-action is="button"></app-step-action>
  </app-step>
</app-steps>
```

The most important part here is the `is` attribute. In Web Components the `is` attribute wasn't actually doing nothing and was being [talked about being removed](https://lists.w3.org/Archives/Public/public-webapps/2015AprJun/0515.html).

I spend a lot of time in the console, iirc the `is` attribute was a part of `HTMLElement.prototype` meaning in chrome's devtools iirc `document.body.is` used to autocomplete and returned `""` but now doesn't autocomplete and returns `undefined`.

My proposal is to have the `is` attribute make that element be the exact same thing as the one specified by the `is` attribute:

Meaning `<app-step-action is="button"></app-step-action>` is the exact same as `<button></button>`

It will be:

- Styled the same
- Have the same `prototype` and `constructor` and the exact same `API`
- Accept the same attribtues

By the last one meaning I can do:

```HTML
<app-step-form is="form">
  <app-step-input is="input" type="text" required autofocus>
  <app-step-action is="button" type="submit"></app-step-action>
</app-step-form>
```

Where `<app-step-input>` will cause the form to show required validivity popup, and autofocus just like a normal `<input>`.

**It will act the exact same way. Essentially be the exact same.**

## Pros
1.My markup is actually **really** semantically written.

2.I don't need to **register** the element via javascript to have the same prototype as the element I want. (Can easily do through my HTML)

Or setting the `is` attribute through javascript:

```JS
var input = document.createElement('app-step-input');
input.is = 'input'; // this will do everything as mentioned above
```

3.I can easily query the `DOM` via **Tag Name** instead of `classes`:

```
var stepInputs = document.getElementsByTagName('app-step-input');
// or
var stepInputs = document.querySelectorAll('app-step-input');
```

So now I can have different `input` elements without having different **classes** or even **IDs**.

4.Classes and IDs are still very usefull.

**HTML:**
```HTML
<app-steps class="flex-container flex">
  <app-step class="flex-container flex">
    <app-step-title is="h1" class="flex"></app-step-title>
    <app-step-info is="span" class="flex></app-step-info>
    <app-step-action is="button" class="flex"></app-step-action>
  </app-step>
  <app-step class="flex-container flex">
    <app-step-title is="h1" class="flex"></app-step-title>
    <app-step-info is="span" class="flex></app-step-info>
    <app-step-action is="button" class="flex"></app-step-action>
  </app-step>
  <app-step class="flex-container flex">
    <app-step-title is="h1" class="flex"></app-step-title>
    <app-step-info is="span" class="flex></app-step-info>
    <app-step-action is="button" class="flex"></app-step-action>
  </app-step>
</app-steps>
```

**CSS:**
```CSS
.flex-container {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.flex {
  flex: 1;
}

app-steps {
 /*Styles*/
}

app-step {
  /*Styles*/
}
```

Yet this is how I would like to really write my `HTML/CSS`, having this **SemanticWEB** where I don't use any classes:

**HTML:**
```HTML
<app-steps>
  <app-step>
    <app-step-title is="h1"></app-step-title>
    <app-step-info is="span"></app-step-info>
    <app-step-action is="button"></app-step-action>
  </app-step>
  <app-step>
    <app-step-title is="h1"></app-step-title>
    <app-step-info is="span"></app-step-info>
    <app-step-action is="button"></app-step-action>
  </app-step>
  <app-step>
    <app-step-title is="h1"></app-step-title>
    <app-step-info is="span"></app-step-info>
    <app-step-action is="button"></app-step-action>
  </app-step>
</app-steps>
```

**CSS:**
```CSS
.flex-container {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.flex {
  flex: 1;
}

app-steps {
 /*Styles*/
 extends: .flex-container, flex;
 /*OR*/
 extends(.flex-container, flex);
}

app-step {
  /*Styles*/
  extends: .flex;
  /*OR*/
  extends(.flex);
}
```

Whichever `extends` would be decided.

The final thing about this proposal is would styling `button { /*styles*/ }` affect the elements that have `is="button"` that's for you guys to decide.

### If your reading this and know someone who would like to put this into action please let's start a discussion in the [issues](https://github.com/eorroe/SemanticWEB/issues)
