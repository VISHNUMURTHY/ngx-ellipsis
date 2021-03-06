# ngx-ellipsis

Plugin for angular (>= 6.0.0) providing a directive to display an ellipsis if the containing text would overflow.

Supports text only (no html contents)!

## Demo

For a demo either just checkout this project and run `npm install && npm run start` or visit [the StackBlitz demo page](https://stackblitz.com/github/lentschi/ngx-ellipsis?file=src%2Fapp%2Fapp.component.html).

## Installation

For use in an existing angular project run `npm install ngx-ellipsis --save`.

Then add the installed module to your `app.module.ts`:

```typescript
import { EllipsisModule } from 'ngx-ellipsis';

// ...

@NgModule({
  // ...
  imports: [
    // ...
    EllipsisModule
  ]
  // ...
})
export class AppModule {}

```

## Usage

Anywhere in your template:

```html
<div style="width: 100px; height: 100px;" ellipsis>Your very long text</div>

<!-- Or for dynamic content: -->
<div style="width: 100px; height: 100px;" ellipsis [ellipsis-content]="yourDynamicContent"></div>
```

As you can see, you need to define the dimensions of your element yourself. (ngx-ellipsis doesn't automatically add any element styles.) But of course you don't need to use fixed widths/heights like in these examples. Flex layout shold work just fine for example.

### Extra options

You may add the following attributes to change the directive's behavior:

| attribute | meaning |
| ---- | ---- |
| __ellipsis__ | _required_ If you pass an attribute value (e.g. `ellipsis=" More ..."`) you can override the text that will be appended, should it be necessary to truncate the text (_default_: "...")|
| __ellipsis-content__ | Use this for dynamic content, that will be subject to asynchronous changes (e.g.: `[ellipsis-content]="myVar"`) |
| __ellipsis-word-boundaries__ | If you pass this attribute, the text won't be truncated at just any character but only at those in the attribute's value. For example `ellipsis-word-boundaries=" \n"` will allow the text to break at spaces and newlines only |
| __ellipsis-resize-detection__ | How resize events should be detected - these are the possible values: <ul><li>__element-resize-detector__: _default_ Use [wnr/element-resize-detector](https://github.com/wnr/element-resize-detector) with its `scroll` strategy. (-> Even when you change the element's width using javascript, the ellipsis will auto-adept)</li><li>__element-resize-detector-object__: _deprecated_ Use [wnr/element-resize-detector](https://github.com/wnr/element-resize-detector) with its `object` strategy</li><li>__window__: Only check if the whole window has been resized/changed orientation by using angular's built-in `HostListener` (Possibly better performance, but obviously won't trigger on resize caused directly or indirectly by javascript.)</li><li>__manual__: Ellipsis is never applied automatically. Instead the consuming app may use `#ell="ellipsis"` in the template and `this.ell.applyEllipsis()` in the component code.</li></ul> |
| __ellipsis-click-more__ | Event emitter - If set, the text defined by the `ellipsis`  attribute will be converted into a clickable link. For example `(ellipsis-click-more)="moreClicked()"` will call your component's `moreClicked()` method when the user clicks on the link.|
| __ellipsis-change__ | Event emitter - Will be emitted whenever the ellipsis has been recalculated (depending on `ellipsis-resize-detection`). If the text had to be truncated the position of the last visible character will be emitted, else `null`.|

## Build & publish on npm

In case you want to contribute/fork:

1. Run `npm install --prefix ./projects/ngx-ellipsis`
1. Adept version and author in `./projects/ngx-ellipsis/package.json`.
1. Run `npm run build-lib` which outputs the build to `./dist/ngx-ellipsis`.
1. Copy README.md to `./dist/ngx-ellipsis` and modify it accordingly.
1. Run `cd ./dist/ngx-ellipsis && npm publish`.


## Running unit tests

Run `npm run test ngx-ellipsis` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Thank you...

- ... __Lucas Wiener__ for writing the [element-resize-detector](https://github.com/wnr/element-resize-detector) package which are internally used by this module.

## License

MIT
