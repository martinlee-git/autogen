# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/dotnet/src/AutoGen.SourceGenerator/README.md
- 미러 경로: `dotnet/src/AutoGen.SourceGenerator/README.md`

## 한글 요약

AutoGen.SourceGenerator 이 패키지는 유형 안전 함수 정의 생성에 대한 지원을 추가하는 소스 생성기를 제공합니다. Function 속성으로 메서드를 표시하기만 하면 소스 생성기가 함수 정의와 함수 호출 래퍼를 생성합니다. 시작하기 먼저 프로젝트 파일에 다음을 추가하고 GenerationDocumentationFile 속성을 true Nightly Build 피드로 설정합니다. https://devdiv.pkgs.visualstudio.com/DevDiv/ Packaging/AutoGen/nuget/v3/index.json 그런 다음 함수 정의 및 함수 호출 래퍼를 생성하려는 메서드에 대해 Function 특성으로 표시합니다. 참고: 최상의 성능을 위해서는 매개 변수 및 반환 유형에 기본 유형을 사용해 보십시오. 소스 생성기는 메서드 서명 및 문서를 기반으로 다음 코드를 생성합니다. 함수 정의를 작성하는 수고를 덜고 실제 메서드 서명으로 최신 상태를 유지하는 데 도움이 됩니다. 더 많은 예제를 보려면 다음 프로젝트 AutoGen.Basic.Samp를 확인하세요.

## 핵심 발췌

파일 AutoGen.SourceGenerator.Tests

## 원문 내용

### AutoGen.SourceGenerator

This package carries a source generator that adds support for type-safe function definition generation. Simply mark a method with `Function` attribute, and the source generator will generate a function definition and a function call wrapper for you.

### Get start

First, add the following to your project file and set `GenerateDocumentationFile` property to true

```xml
<PropertyGroup>
    <!-- This enables structural xml document support -->
    <GenerateDocumentationFile>true</GenerateDocumentationFile>
</PropertyGroup>
```
```xml
<ItemGroup>
    <PackageReference Include="AutoGen.SourceGenerator" />
</ItemGroup>
```

> Nightly Build feed: https://devdiv.pkgs.visualstudio.com/DevDiv/_packaging/AutoGen/nuget/v3/index.json

Then, for the methods you want to generate function definition and function call wrapper, mark them with `Function` attribute:

> Note: For the best of performance, try using primitive types for the parameters and return type.

```csharp
// file: MyFunctions.cs

using AutoGen;

// a partial class is required
// and the class must be public
public partial class MyFunctions
{
    /// <summary>
    /// Add two numbers.
    /// </summary>
    /// <param name="a">The first number.</param>
    /// <param name="b">The second number.</param>
    [Function]
    public Task<string> AddAsync(int a, int b)
    {
        return Task.FromResult($"{a} + {b} = {a + b}");
    }
}
```

The source generator will generate the following code based on the method signature and documentation. It helps you save the effort of writing function definition and keep it up to date with the actual method signature.

```csharp
// file: MyFunctions.generated.cs
public partial class MyFunctions
{
    private class AddAsyncSchema
    {
		public int a {get; set;}
		public int b {get; set;}
    }

    public Task<string> AddAsyncWrapper(string arguments)
    {
        var schema = JsonSerializer.Deserialize<AddAsyncSchema>(
            arguments, 
            new JsonSerializerOptions
            {
                PropertyNamingPolicy = JsonNamingPolicy.CamelCase,
            });
        return AddAsync(schema.a, schema.b);
    }

    public FunctionDefinition AddAsyncFunction
    {
        get => new FunctionDefinition
		{
			Name = @"AddAsync",
            Description = """
Add two numbers.
""",
            Parameters = BinaryData.FromObjectAsJson(new
            {
                Type = "object",
                Properties = new
				{
				    a = new
				    {
					    Type = @"number",
					    Description = @"The first number.",
				    },
				    b = new
				    {
					    Type = @"number",
					    Description = @"The second number.",
				    },
                },
                Required = new []
				{
				    "a",
				    "b",
				},
            },
            new JsonSerializerOptions
			{
				PropertyNamingPolicy = JsonNamingPolicy.CamelCase,
			})
        };
    }
}
```

For more examples, please check out the following project
- [AutoGen.Basic.Sample](../samples/AgentChat/Autogen.Basic.Sample/)
- [AutoGen.SourceGenerator.Tests](../../test/AutoGen.SourceGenerator.Tests/)