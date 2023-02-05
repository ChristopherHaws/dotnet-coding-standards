# Chaws' Coding Standards
This repo is a place for me to keep all my shared configuration between projects in one place. These configurations are very opinionated to fit the way I like to work.

> Since this is an internal tool for my personal projects, new features will be enabled by default and versioning will **not** follow `semver`.


## Usage
```xml
<!-- Directory.Build.props -->
<Project>

	<!-- Required Properties -->
	<PropertyGroup>
		<!-- Product name information for the assembly manifest -->
		<Product>My Awesome Project</Product>

		<!-- A comma-separated list of NuGet packages authors -->
		<Authors>Christopher.Haws</Authors>

		<!-- The name of the copyright holder -->
		<CopyrightHolder>Christopher Haws</CopyrightHolder>
	</PropertyGroup>

	<!-- Optional Properties -->
	<PropertyGroup>
		<!-- -->
		<Company>Contoso</Company>

		<!-- -->
		<Company>Contoso</Company>
	</PropertyGroup>

</Project>
```


## Roadmap
- [ ] - Add logging to log changed features (toggleable)
- [ ] - Add the ability to build containers via `EnableSdkContainerSupport`
- [ ] - Look into if it is possible to detect installed packages and enable/disable features based on that


## Features

### Reproducible Builds
![License](https://img.shields.io/github/license/dotnet/reproducible-builds)
![Nuget](https://img.shields.io/nuget/v/DotNet.ReproducibleBuilds.Isolated)
![GitHub Stars](https://img.shields.io/github/stars/dotnet/reproducible-builds?logo=github)

These packages are used to:
- keep builds idempotent
- sets a bunch of properties based on the CI pipeline you use to help keep your builds consistent across platforms
- sets up [SourceLink](https://github.com/dotnet/sourcelink) on your build to make it [easier to debug](https://devblogs.microsoft.com/dotnet/improving-debug-time-productivity-with-source-link/) into your project's source code
- prevents the build from unintentionally depending on other installed software that's not described by your repo
- other cool things! Go check out their github for more info! :)


### Preconfigured Static Analysis
I like to live on the edge in my personal projects so I have the analysis level set to `preview`. If you prefer to set the level to something else, you can do so by setting this value yourself:
```xml
<PropertyGroup>
	<AnalysisLevel>latest</AnalysisLevel>
<PropertyGroup>
```

#### Microsoft.VisualStudio.Threading.Analyzers
![License](https://img.shields.io/github/license/dotnet/roslyn-analyzers)
![Nuget](https://img.shields.io/nuget/v/Microsoft.VisualStudio.Threading.Analyzers)
![GitHub Stars](https://img.shields.io/github/stars/dotnet/roslyn-analyzers?logo=github)


#### Microsoft.CodeAnalysis.PublicApiAnalyzers
![License](https://img.shields.io/github/license/dotnet/roslyn-analyzers)
![Nuget](https://img.shields.io/nuget/v/Microsoft.CodeAnalysis.PublicApiAnalyzers)
![GitHub Stars](https://img.shields.io/github/stars/dotnet/roslyn-analyzers?logo=github)

This package contains rules to help library authors monitoring change to their public APIs.


#### Microsoft.CodeAnalysis.BannedApiAnalyzers
![License](https://img.shields.io/github/license/dotnet/roslyn-analyzers)
![Nuget](https://img.shields.io/nuget/v/Microsoft.CodeAnalysis.BannedApiAnalyzers)
![GitHub Stars](https://img.shields.io/github/stars/dotnet/roslyn-analyzers?logo=github)

**Purpose**
Allows banning the use of arbitrary code using a txt file.

**Relavent Files**
[BannedSymbolsFile](/src/files/BannedSymbols.txt)

**Disable**
```xml
<PropertyGroup>
	<IncludeDefaultBannedSymbols>false</IncludeDefaultBannedSymbols>
</PropertyGroup>
```

#### Microsoft.CodeAnalysis.NetAnalyzers
![License](https://img.shields.io/github/license/dotnet/roslyn-analyzers)
![Nuget](https://img.shields.io/nuget/v/Microsoft.CodeAnalysis.NetAnalyzers)
![GitHub Stars](https://img.shields.io/github/stars/dotnet/roslyn-analyzers?logo=github)

This is the default analyzer that ships with .NET. Including it manually means we will get updates without needing to update .NET.

#### Nullable.Extended.Analyzer
![License](https://img.shields.io/github/license/tom-englert/nullable.extended)
![Nuget](https://img.shields.io/nuget/v/Nullable.Extended.Analyzer)
![GitHub Stars](https://img.shields.io/github/stars/tom-englert/nullable.extended?logo=github)

**Disable**
```xml
<PropertyGroup>
	<DisableNullableExtendedAnalyzer>true</DisableNullableExtendedAnalyzer>
</PropertyGroup>
```

#### Meziantou.Analyzer
![License](https://img.shields.io/github/license/dotnet/roslyn-analyzers)
![Nuget](https://img.shields.io/nuget/v/Meziantou.Analyzer)
![GitHub Stars](https://img.shields.io/github/stars/meziantou/Meziantou.Analyzer?logo=github)


### JetBrains Annotations
This meta package adds `JetBrains.Annotations` and adds it's namespace to the implicit usings.


### Access internal types with UnitTests
This package allows you to access internal types in tests as long as you name your test project `{ProjectName}.Tests`


### Access internal types with LINQPad durring development
I use LINQPad a lot during development for prototyping and experimenting. Being able to reference my assemplies and use the internal types is very handy!

## Building
```shell
nuget pack Chaws.DotNet.CodingStandards.nuspec -ForceEnglishOutput -Version 1.0.0
```

## Build-in SDK Properties and Items
- [Microsoft.NET.Sdk](https://learn.microsoft.com/en-us/dotnet/core/project-sdk/msbuild-props#runtime-configuration-properties)

## References
- [Sharing coding style and Roslyn analyzers across projects](https://www.meziantou.net/sharing-coding-style-and-roslyn-analyzers-across-projects.htm) [Source code](https://github.com/meziantou/Meziantou.DotNet.CodingStandard)
- [MSBuild `.props` and `.targets` in a package](https://learn.microsoft.com/en-us/nuget/concepts/msbuild-props-and-targets)
- [MSBuild Project element](https://learn.microsoft.com/en-us/visualstudio/msbuild/project-element-msbuild?view=vs-2022)
- [EditorConfig vs global analyzer configuration](https://github.com/dotnet/roslyn/issues/47707)
- [MSBuild Advanced Concepts](https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild-advanced-concepts?view=vs-2022)
