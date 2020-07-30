---
title: project.jsporównanie i csproj
description: Zobacz mapowanie między elementami project.json i csproj.
author: natemcmaster
ms.date: 03/13/2017
ms.openlocfilehash: c8638bc30ba09d8e8d464159aded60dcde4b8dc0
ms.sourcegitcommit: 32f0d6f4c01ddc6ca78767c3a30e3305f8cd032c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2020
ms.locfileid: "87427024"
---
# <a name="a-mapping-between-projectjson-and-csproj-properties"></a>Mapowanie między project.jswłaściwościami i csproj

Według [McMaster](https://github.com/natemcmaster)

Podczas opracowywania narzędzi programu .NET Core wprowadzono ważną zmianę projektową, która nie obsługuje już *project.jsw* plikach i zamiast tego przenosi projekty .NET Core do formatu MSBuild/csproj.

W tym artykule przedstawiono sposób, w jaki ustawienia w *project.jsna* są reprezentowane w formacie MSBuild/csproj, dzięki czemu można dowiedzieć się, jak używać nowego formatu i zrozumieć zmiany wprowadzone przez narzędzia migracji w przypadku uaktualniania projektu do najnowszej wersji narzędzi.

## <a name="the-csproj-format"></a>Format csproj

Nowy format, \* . csproj, jest formatem opartym na formacie XML. Poniższy przykład przedstawia węzeł główny projektu .NET Core przy użyciu `Microsoft.NET.Sdk` . W przypadku projektów sieci Web używany jest zestaw SDK `Microsoft.NET.Sdk.Web` .

```xml
<Project Sdk="Microsoft.NET.Sdk">
...
</Project>
```

## <a name="common-top-level-properties"></a>Wspólne właściwości najwyższego poziomu

### <a name="name"></a>name

```json
{
  "name": "MyProjectName"
}
```

Nie jest już obsługiwane. W csproj jest to określane przez nazwę pliku projektu, która zwykle jest zgodna z nazwą katalogu. Na przykład `MyProjectName.csproj`.

Domyślnie nazwa pliku projektu określa również wartość `<AssemblyName>` `<PackageId>` właściwości i.

```xml
<PropertyGroup>
  <AssemblyName>MyProjectName</AssemblyName>
  <PackageId>MyProjectName</PackageId>
</PropertyGroup>
```

`<AssemblyName>`Właściwość ma inną wartość niż `<PackageId>` `buildOptions\outputName` w przypadku zdefiniowania właściwości w project.js.
Aby uzyskać więcej informacji, zobacz [inne typowe opcje kompilacji](#other-common-build-options).

### <a name="version"></a>version

```json
{
  "version": "1.0.0-alpha-*"
}
```

Użyj `VersionPrefix` właściwości i `VersionSuffix` :

```xml
<PropertyGroup>
  <VersionPrefix>1.0.0</VersionPrefix>
  <VersionSuffix>alpha</VersionSuffix>
</PropertyGroup>
```

Można również użyć `Version` właściwości, ale może to spowodować zastąpienie ustawień wersji podczas pakowania:

```xml
<PropertyGroup>
  <Version>1.0.0-alpha</Version>
</PropertyGroup>
```

### <a name="other-common-root-level-options"></a>Inne typowe opcje poziomu głównego

```json
{
  "authors": [ "Anne", "Bob" ],
  "company": "Contoso",
  "language": "en-US",
  "title": "My library",
  "description": "This is my library.\r\nAnd it's really great!",
  "copyright": "Nugetizer 3000",
  "userSecretsId": "xyz123"
}
```

```xml
<PropertyGroup>
  <Authors>Anne;Bob</Authors>
  <Company>Contoso</Company>
  <NeutralLanguage>en-US</NeutralLanguage>
  <AssemblyTitle>My library</AssemblyTitle>
  <Description>This is my library.
And it's really great!</Description>
  <Copyright>Nugetizer 3000</Copyright>
  <UserSecretsId>xyz123</UserSecretsId>
</PropertyGroup>
```

## <a name="frameworks"></a>platform

### <a name="one-target-framework"></a>Jedna platforma docelowa

```json
{
  "frameworks": {
    "netcoreapp1.0": {}
  }
}
```

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp1.0</TargetFramework>
</PropertyGroup>
```

### <a name="multiple-target-frameworks"></a>Wiele platform docelowych

```json
{
  "frameworks": {
    "netcoreapp1.0": {},
    "net451": {}
  }
}
```

Użyj `TargetFrameworks` właściwości, aby zdefiniować listę platform docelowych. Użyj średnika, aby oddzielić wiele wartości struktury.

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp1.0;net451</TargetFrameworks>
</PropertyGroup>
```

## <a name="dependencies"></a>zależności

> [!IMPORTANT]
> Jeśli zależność jest **projektem** , a nie pakietem, format jest inny.
> Aby uzyskać więcej informacji, zobacz sekcję [Typ zależności](#dependency-type) .

### <a name="netstandardlibrary-metapackage"></a>Biblioteka servicepackage. Library

```json
{
  "dependencies": {
    "NETStandard.Library": "1.6.0"
  }
}
```

```xml
<PropertyGroup>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

### <a name="microsoftnetcoreapp-metapackage"></a>Pakiet Microsoft. servicecore. App

```json
{
  "dependencies": {
    "Microsoft.NETCore.App": "1.0.0"
  }
}
```

```xml
<PropertyGroup>
  <RuntimeFrameworkVersion>1.0.3</RuntimeFrameworkVersion>
</PropertyGroup>
```

`<RuntimeFrameworkVersion>`Wartość w migrowanym projekcie jest określana na podstawie zainstalowanej wersji zestawu SDK.

### <a name="top-level-dependencies"></a>Zależności najwyższego poziomu

```json
{
  "dependencies": {
    "Microsoft.AspNetCore": "1.1.0"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore" Version="1.1.0" />
</ItemGroup>
```

### <a name="per-framework-dependencies"></a>Zależności dla architektury

```json
{
  "framework": {
    "net451": {
      "dependencies": {
        "System.Collections.Immutable": "1.3.1"
      }
    },
    "netstandard1.5": {
      "dependencies": {
        "Newtonsoft.Json": "9.0.1"
      }
    }
  }
}
```

```xml
<ItemGroup Condition="'$(TargetFramework)'=='net451'">
  <PackageReference Include="System.Collections.Immutable" Version="1.3.1" />
</ItemGroup>

<ItemGroup Condition="'$(TargetFramework)'=='netstandard1.5'">
  <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
</ItemGroup>
```

### <a name="imports"></a>importy

```json
{
  "dependencies": {
    "YamlDotNet": "4.0.1-pre309"
  },
  "frameworks": {
    "netcoreapp1.0": {
      "imports": [
        "dnxcore50",
        "dotnet"
      ]
    }
  }
}
```

```xml
<PropertyGroup>
  <PackageTargetFallback>dnxcore50;dotnet</PackageTargetFallback>
</PropertyGroup>
<ItemGroup>
  <PackageReference Include="YamlDotNet" Version="4.0.1-pre309" />
</ItemGroup>
```

### <a name="dependency-type"></a>Typ zależności

#### <a name="type-project"></a>Typ: projekt

```json
{
  "dependencies": {
    "MyOtherProject": "1.0.0-*",
    "AnotherProject": {
      "type": "project"
    }
  }
}
```

```xml
<ItemGroup>
  <ProjectReference Include="..\MyOtherProject\MyOtherProject.csproj" />
  <ProjectReference Include="..\AnotherProject\AnotherProject.csproj" />
</ItemGroup>
```

> [!NOTE]
> Spowoduje to przerwanie sposobu `dotnet pack --version-suffix $suffix` określania wersji zależności odwołania do projektu.

#### <a name="type-build"></a>Typ: kompilacja

```json
{
  "dependencies": {
    "Microsoft.EntityFrameworkCore.Design": {
      "version": "1.1.0",
      "type": "build"
    }
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="1.1.0" PrivateAssets="All" />
</ItemGroup>
```

#### <a name="type-platform"></a>Typ: platforma

```json
{
  "dependencies": {
    "Microsoft.NETCore.App": {
      "version": "1.1.0",
      "type": "platform"
    }
  }
}
```

Nie ma odpowiednika w csproj.

## <a name="runtimes"></a>Runtime

```json
{
  "runtimes": {
    "win7-x64": {},
    "osx.10.11-x64": {},
    "ubuntu.16.04-x64": {}
  }
}
```

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win7-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="standalone-apps-self-contained-deployment"></a>Aplikacje autonomiczne (wdrażanie samodzielne)

W project.jsna definiowanie `runtimes` sekcji oznacza, że aplikacja była autonomiczna podczas kompilowania i publikowania.
W programie MSBuild wszystkie projekty są *przenośne* podczas kompilacji, ale można je opublikować jako autonomiczną.

`dotnet publish --framework netcoreapp1.0 --runtime osx.10.11-x64`

Aby uzyskać więcej informacji, zobacz artykuły [z obsługą prewartą (SCD)](../deploying/index.md#publish-self-contained).

## <a name="tools"></a>tools

```json
{
  "tools": {
    "Microsoft.EntityFrameworkCore.Tools.DotNet": "1.0.0-*"
  }
}
```

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="1.0.0" />
</ItemGroup>
```

> [!NOTE]
> `imports`narzędzia nie są obsługiwane w programie csproj. Narzędzia, które wymagają importu, nie będą działały z nowym `Microsoft.NET.Sdk` .

## <a name="buildoptions"></a>buildOptions

Zobacz również [pliki](#files).

### <a name="emitentrypoint"></a>emitEntryPoint

```json
{
  "buildOptions": {
    "emitEntryPoint": true
  }
}
```

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

Jeśli `emitEntryPoint` była `false` , wartość `OutputType` jest konwertowana na `Library` , która jest wartością domyślną:

```json
{
  "buildOptions": {
    "emitEntryPoint": false
  }
}
```

```xml
<PropertyGroup>
  <OutputType>Library</OutputType>
  <!-- or, omit altogether. It defaults to 'Library' -->
</PropertyGroup>
```

### <a name="keyfile"></a>keyFile

```json
{
  "buildOptions": {
    "keyFile": "MyKey.snk"
  }
}
```

`keyFile`Element rozwija do trzech właściwości w programie MSBuild:

```xml
<PropertyGroup>
  <AssemblyOriginatorKeyFile>MyKey.snk</AssemblyOriginatorKeyFile>
  <SignAssembly>true</SignAssembly>
  <PublicSign Condition="'$(OS)' != 'Windows_NT'">true</PublicSign>
</PropertyGroup>
```

### <a name="other-common-build-options"></a>Inne typowe opcje kompilacji

```json
{
  "buildOptions": {
    "warningsAsErrors": true,
    "nowarn": ["CS0168", "CS0219"],
    "xmlDoc": true,
    "preserveCompilationContext": true,
    "outputName": "Different.AssemblyName",
    "debugType": "portable",
    "allowUnsafe": true,
    "define": ["TEST", "OTHERCONDITION"]
  }
}
```

```xml
<PropertyGroup>
  <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
  <NoWarn>$(NoWarn);CS0168;CS0219</NoWarn>
  <GenerateDocumentationFile>true</GenerateDocumentationFile>
  <PreserveCompilationContext>true</PreserveCompilationContext>
  <AssemblyName>Different.AssemblyName</AssemblyName>
  <DebugType>portable</DebugType>
  <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
  <DefineConstants>$(DefineConstants);TEST;OTHERCONDITION</DefineConstants>
</PropertyGroup>
```

## <a name="packoptions"></a>packOptions

Zobacz również [pliki](#files).

### <a name="common-pack-options"></a>Opcje wspólnego pakietu

```json
{
  "packOptions": {
    "summary": "numl is a machine learning library intended to ease the use of using standard modeling techniques for both prediction and clustering.",
    "tags": ["machine learning", "framework"],
    "releaseNotes": "Version 0.9.12-beta",
    "iconUrl": "http://numl.net/images/ico.png",
    "projectUrl": "http://numl.net",
    "licenseUrl": "https://raw.githubusercontent.com/sethjuarez/numl/master/LICENSE.md",
    "requireLicenseAcceptance": false,
    "repository": {
      "type": "git",
      "url": "https://raw.githubusercontent.com/sethjuarez/numl"
    },
    "owners": ["Seth Juarez"]
  }
}
```

```xml
<PropertyGroup>
  <!-- summary is not migrated from project.json, but you can use the <Description> property for that if needed. -->
  <PackageTags>machine learning;framework</PackageTags>
  <PackageReleaseNotes>Version 0.9.12-beta</PackageReleaseNotes>
  <PackageIcon>ico.png</PackageIcon>
  <PackageProjectUrl>http://numl.net</PackageProjectUrl>
  <PackageLicenseUrl>https://raw.githubusercontent.com/sethjuarez/numl/master/LICENSE.md</PackageLicenseUrl>
  <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
  <RepositoryType>git</RepositoryType>
  <RepositoryUrl>https://raw.githubusercontent.com/sethjuarez/numl</RepositoryUrl>
  <!-- owners is not supported in MSBuild -->
</PropertyGroup>
```

Nie ma odpowiednika dla `owners` elementu w programie MSBuild. W przypadku programu `summary` można użyć właściwości programu MSBuild `<Description>` . Wartość `summary` nie jest automatycznie migrowana do tej właściwości, ponieważ ta właściwość jest zamapowana na [`description`](#other-common-root-level-options) element.  [PackageIconUrl jest przestarzała](/nuget/reference/msbuild-targets#packageiconurl) na rzecz PackageIcon.

## <a name="scripts"></a>skrypty

```json
{
  "scripts": {
    "precompile": "generateCode.cmd",
    "postpublish": [ "obfuscate.cmd", "removeTempFiles.cmd" ]
  }
}
```

Ich odpowiedniki w programie MSBuild są [obiektami docelowymi](/visualstudio/msbuild/msbuild-targets):

```xml
<Target Name="MyPreCompileTarget" BeforeTargets="Build">
  <Exec Command="generateCode.cmd" />
</Target>

<Target Name="MyPostCompileTarget" AfterTargets="Publish">
  <Exec Command="obfuscate.cmd" />
  <Exec Command="removeTempFiles.cmd" />
</Target>
```

## <a name="runtimeoptions"></a>runtimeOptions

```json
{
  "runtimeOptions": {
    "configProperties": {
      "System.GC.Server": true,
      "System.GC.Concurrent": true,
      "System.GC.RetainVM": true,
      "System.Threading.ThreadPool.MinThreads": 4,
      "System.Threading.ThreadPool.MaxThreads": 25
    }
  }
}
```

Wszystkie ustawienia w tej grupie, z wyjątkiem `System.GC.Server` właściwości, są umieszczane w pliku o nazwie *runtimeconfig.template.jsw* folderze projektu, z opcjami podniesionymi do obiektu głównego podczas procesu migracji:

```json
{
  "configProperties": {
    "System.GC.Concurrent": true,
    "System.GC.RetainVM": true,
    "System.Threading.ThreadPool.MinThreads": 4,
    "System.Threading.ThreadPool.MaxThreads": 25
  }
}
```

`System.GC.Server`Właściwość jest migrowana do pliku CSPROJ:

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

Można jednak ustawić wszystkie te wartości w csproj, a także właściwości programu MSBuild:

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
  <ConcurrentGarbageCollection>true</ConcurrentGarbageCollection>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
  <ThreadPoolMaxThreads>25</ThreadPoolMaxThreads>
</PropertyGroup>
```

## <a name="shared"></a>udostępnione

```json
{
  "shared": "shared/**/*.cs"
}
```

Nieobsługiwane w csproj. Zamiast tego Utwórz dołączenie plików zawartości w pliku *. nuspec* .
Aby uzyskać więcej informacji, zobacz [Dołączanie plików zawartości](/nuget/schema/nuspec#including-content-files).

## <a name="files"></a>files

W *project.jsw systemie*kompilacja i pakiet można rozszerzyć, aby kompilować i osadzać z różnych folderów.
W programie MSBuild odbywa się to za pomocą [elementów](/visualstudio/msbuild/common-msbuild-project-items). Poniższy przykład jest wspólną konwersją:

```json
{
  "buildOptions": {
    "compile": {
      "copyToOutput": "notes.txt",
      "include": "../Shared/*.cs",
      "exclude": "../Shared/Not/*.cs"
    },
    "embed": {
      "include": "../Shared/*.resx"
    }
  },
  "packOptions": {
    "include": "Views/",
    "mappings": {
      "some/path/in/project.txt": "in/package.txt"
    }
  },
  "publishOptions": {
    "include": [
      "files/",
      "publishnotes.txt"
    ]
  }
}
```

```xml
<ItemGroup>
  <Compile Include="..\Shared\*.cs" Exclude="..\Shared\Not\*.cs" />
  <EmbeddedResource Include="..\Shared\*.resx" />
  <Content Include="Views\**\*" PackagePath="%(Identity)" />
  <None Include="some/path/in/project.txt" Pack="true" PackagePath="in/package.txt" />
  
  <None Include="notes.txt" CopyToOutputDirectory="Always" />
  <!-- CopyToOutputDirectory = { Always, PreserveNewest, Never } -->

  <Content Include="files\**\*" CopyToPublishDirectory="PreserveNewest" />
  <None Include="publishnotes.txt" CopyToPublishDirectory="Always" />
  <!-- CopyToPublishDirectory = { Always, PreserveNewest, Never } -->
</ItemGroup>
```

> [!NOTE]
> Wiele domyślnych [wzorców obsługi symboli wieloznacznych](https://en.wikipedia.org/wiki/Glob_(programming)) są automatycznie dodawane przez zestaw .NET Core SDK. Aby uzyskać więcej informacji, zobacz [Domyślna kompilacja zawiera](../project-sdk/overview.md#default-compilation-includes).

Wszystkie `ItemGroup` elementy MSBuild obsługują `Include` , `Exclude` i `Remove` .

Układ pakietu wewnątrz. nupkg można modyfikować za pomocą `PackagePath="path"` .

Z wyjątkiem `Content` , większość grup elementów wymaga jawnego dodania `Pack="true"` do pakietu. `Content`zostanie umieszczony w folderze *zawartości* pakietu, ponieważ `<IncludeContentInPack>` właściwość MSBuild jest domyślnie ustawiona na wartość `true` .
Aby uzyskać więcej informacji, zobacz temat [uwzględnianie zawartości w pakiecie](/nuget/schema/msbuild-targets#including-content-in-a-package).

`PackagePath="%(Identity)"`to krótka metoda ustawiania ścieżki pakietu do ścieżki pliku względnej dla projektu.

## <a name="testrunner"></a>testRunner

### <a name="xunit"></a>xUnit

```json
{
  "testRunner": "xunit",
  "dependencies": {
    "dotnet-test-xunit": "<any>"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-*" />
  <PackageReference Include="xunit" Version="2.2.0-*" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0-*" />
</ItemGroup>
```

### <a name="mstest"></a>MSTest

```json
{
  "testRunner": "mstest",
  "dependencies": {
    "dotnet-test-mstest": "<any>"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-*" />
  <PackageReference Include="MSTest.TestAdapter" Version="1.1.12-*" />
  <PackageReference Include="MSTest.TestFramework" Version="1.1.11-*" />
</ItemGroup>
```

## <a name="see-also"></a>Zobacz też

- [Ogólne omówienie zmian w interfejsie wiersza polecenia](cli-msbuild-architecture.md)
