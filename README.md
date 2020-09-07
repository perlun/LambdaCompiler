# LambdaCompiler

This is an attempt at getting `System.Linq.Expressions.Compiler.LambdaCompiler` working on .NET Core 3.1.

The effort was started after reading [this SO post](https://stackoverflow.com/a/41678497/227779); I decided to give this a look and see how hard it would be.

Unfortunately, it is non-trivial because of (at least) the following issues:

* `AppDomain.CurrentDomain.DefineDynamicAssembly` is unavailable in .NET Core - `AssemblyBuilder.DefineDynamicAssembly` replaces is. [This SO answer](https://stackoverflow.com/a/36937598/227779) describes how it can be used.
- `Assembly.DefineVersionInfoResource` is unavailable.
- Reliance on internal methods and properties, for example `BlockExpression.ExpressionCount`, `BlockExpression.GetExpression`, `BinaryExpression.IsLiftedLogical` etc.

For the reasons given above, an attempt to make this work as a standalone package is quite unfruitful in nature. The only realistic way to get this working would be to include it in .NET Core proper.

This, however, is problematic for other reasons. I believe the licensing is one of the stumbling stones here. Some of this code was probably written as part of the [DLR effort](https://github.com/IronLanguages/dlr), which it itself Apache-licensed. As soon as you have contributions from 3rd party contributors in the code base, relicensing it (to MIT, like the rest of the .NET Core codebase) becomes more or less impossible.

## License

[Apache 2.0](LICENSE)
