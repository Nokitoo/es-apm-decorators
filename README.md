# es-apm-decorators

The [Elasticsearch APM Node API](https://www.elastic.co/guide/en/apm/agent/nodejs/current/index.html)
is great for automatically plugging into various existing
frameworks, but can be a little verbose to add your own
custom spans and such.  This package provides decorators
to let you easily get more insight into your systems.

## Installation

```bash
npm install --save es-apm-decorators
```

## Usage

You can apply the `@Span()` decorator to class methods.  Class
methods that are `async` will be correctly handled, with the span
ending after the `async` call returns.

```typescript
import { Span } from 'es-apm-decorators';

class MyClass {
	// By default, this will create a span in the current
	// transaction named 'MyClass.doSomething' with the
	// type MyClass.
	@Span()
	public doSomething() {
		// Do something interesting...
	}

	// You can override either name or type, or both at once.
	@Span({ name: 'BigTransaction', type: 'db' })
	public async interactWithDatabase() {
		// Do some big database transaction...
	}
}
```

## Error handling

If a decorated method throws any errors, the current transaction
will be marked with an 'error' result.

*TODO:* Make this more configurable

