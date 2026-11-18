### Just run this on your browser: 

```js
(function disableAntiDebugging() {
    const originalFunctionConstructor = window.Function;

    window.Function = new Proxy(originalFunctionConstructor, {
        apply(target, thisArgument, argumentsList) {
            const sanitizedArguments = argumentsList.map(argument =>
                typeof argument === "string"
                    ? argument.replace(/\bdebugger\s*;?/g, "")
                    : argument
            );

            return Reflect.apply(target, thisArgument, sanitizedArguments);
        },

        construct(target, argumentsList, newTarget) {
            const sanitizedArguments = argumentsList.map(argument =>
                typeof argument === "string"
                    ? argument.replace(/\bdebugger\s*;?/g, "")
                    : argument
            );

            return Reflect.construct(target, sanitizedArguments, newTarget);
        }
    });
})();

```





