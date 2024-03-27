# dotnet8_wpf_blazor_example2

## がんばり中
* (目標) できるだけ同じスキル (C# + Blazor) で Web もデスクトップもモバイルも開発できる構成を作る
* Web アプリもデスクトップアプリも View は Blazor を使う
* View (Blazor) は Server と Wpf の両方から同じファイルを使用できるようにする
* 開発は Linux コンテナにローカルの VSCode から RemoteSSH で接続して行う
* デスクトップアプリの場合も、View (Blazor) + Server で 8 割方開発できるようにする
* デスクトップアプリの場合も、View の自動テストが行えるようにする

[.NET 8 の ASP.NET Core Blazor 新機能オーバービュー](https://zenn.dev/microsoft/articles/aspnetcore-blazor-dotnet8-overview)  
[Blazor で HTML を書きたくないよぉ…(Fluent UI Blazor 編 on .NET 8)](https://zenn.dev/microsoft/articles/aspnetcore-blazor-dotnet8-fluentui)  
[Windows Presentation Foundation (WPF) の Blazor アプリを構築する](https://learn.microsoft.com/ja-jp/aspnet/core/blazor/hybrid/tutorials/wpf?view=aspnetcore-8.0)  
[BlazorWebView WPF Tutorial.](https://jspuij.github.io/BlazorWebView.Docs/pages/wpftutorial.html?tabs=addwpf-1)  

```
> dotnet --info
.NET SDK:
 Version:           8.0.202
 Commit:            25674bb2f4
 Workload version:  8.0.200-manifests.a7f084b6

ランタイム環境:
 OS Name:     Windows
 OS Version:  10.0.19045
 OS Platform: Windows
 RID:         win-x64
 Base Path:   C:\Program Files\dotnet\sdk\8.0.202\
```

```
dotnet new blazorserver -o BlazorServer
dotnet new blazor --interactivity Server -o BlazorWebApp
dotnet new wpf -o BlazorWpfApp
```

```
dotnet run --project BlazorServer
dotnet run --project BlazorWebApp
dotnet run --project BlazorWpfApp
```

```
> dotnet new blazor --help
Blazor Web アプリ (C#)
作成者: Microsoft
説明: サーバー側のレンダリングとクライアントの対話機能の両方をサポートする Blazor Web アプリを作成するためのプロジェクト テンプレートです。このテンプレートは、リッチな動的ユーザー インターフェイス (UI) を持つ Web ア
プリに使用できます。
このテンプレートには、Microsoft 以外のパーティのテクノロジーが含まれています。詳しくは、https://aka.ms/aspnetcore/8.0-third-party-notices をご覧ください。

使用法:
  dotnet new blazor [options] [テンプレート オプション]

オプション:
  -n, --name <name>       作成される出力の名前です。名前を指定しない場合は、出力ディレクトリの名前が使用されます。
  -o, --output <output>   生成された出力を配置する場所。
  --dry-run               指定されたコマンドラインがテンプレートを実行した場合に発生する結果の概要を表示します。
  --force                 既存のファイルが変更された場合でも、コンテンツを強制的に生成します。
  --no-update-check       テンプレートをインスタンス化する場合に、テンプレート パッケージの更新の確認を無効にします。
  --project <project>     コンテキストの評価に使用する必要があるプロジェクトです。
  -lang, --language <C#>  テンプレート言語を指定してインスタンスを作成します。
  --type <project>        テンプレートの種類を指定してインスタンスを作成します。

テンプレート オプション:
  -f, --framework <net8.0>                              プロジェクトのターゲット フレームワークです。
                                                        種類: choice
                                                          net8.0  ターゲット net8.0
                                                        既定: net8.0
  --no-restore                                          指定した場合、作成時にプロジェクトの自動復元がスキップされます。
                                                        種類: bool
                                                        既定: false
  --exclude-launch-settings                             生成されたテンプレートから launchSettings.json を除外するかどうか。
                                                        種類: bool
                                                        既定: false
  -int, --interactivity <Auto|None|Server|WebAssembly>  対話型コンポーネントに使用するホスティング プラットフォームを選択します
                                                        種類: choice
                                                          None         インタラクティビティなし (静的サーバー レンダリングのみ)
                                                          Server       サーバーで実行
                                                          WebAssembly  WebAssembly を使用してブラウザーで実行します
                                                          Auto         WebAssembly 資産のダウンロード中にサーバーを使用してから、WebAssembly を使用します
                                                        既定: Server
  -e, --empty                                           基本的な使用パターンを示すサンプル ページとスタイルを省略するかどうかを構成します。
                                                        種類: bool
                                                        既定: false
  -au, --auth <Individual|None>                         使用する認証の種類
                                                        種類: choice
                                                          None        認証なし
                                                          Individual  個別の認証
                                                        既定: None
  -uld, --use-local-db                                  SQLite の代わりに LocalDB を使用するかどうか。このオプションは、--auth Individual が指定されている場合にのみ適用されます。
                                                        種類: bool
                                                        既定: false
  -ai, --all-interactive                                最上位レベルで対話型レンダリング モードを適用して、すべてのページを対話型にするかどうかを構成します。false の場合、ページは既定で静的サーバー レンダリングを使 
用し、ページ単位またはコンポーネント単位で対話型としてマークできます。
                                                        有効な場合: (InteractivityPlatform != "None")
                                                        種類: bool
                                                        既定: false
  --no-https                                            HTTPS をオフにするかどうか。このオプションは、Individual が --auth に使用されていない場合にのみ適用されます。
                                                        種類: bool
                                                        既定: false
  --use-program-main                                    最上位レベルのステートメントではなく、明示的な Program クラスと Main メソッドを生成するかどうか。
                                                        種類: bool
                                                        既定: false

```

```
dotnet add BlazorWpfApp package Microsoft.AspNetCore.Components.WebView.Wpf
```

BlazorWpfApp\BlazorWpfApp.csproj
```xml
<Project Sdk="Microsoft.NET.Sdk.Razor">　★★★

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net8.0-windows</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <UseWPF>true</UseWPF>
    <RootNamespace>BlazorWpfApp</RootNamespace>　★★★
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.Components.WebView.Wpf" Version="8.0.14" />
  </ItemGroup>

</Project>
```