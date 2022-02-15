# WinAppDriver UI Recorder Tool

This tool allows UI element inspection and generates an XPath query to the element. More information can be found on the [wiki](https://github.com/Microsoft/WinAppDriver/wiki/WinAppDriver-UI-Recorder).


## Requirements

- Windows 10 PC with the latest Windows 10 version (Version 1607 or later)
- Microsoft Visual Studio 2017 or later


## Getting Started

1. Open `WinAppDriverUIRecorder.sln` in Visual Studio
2. Select **Debug** > **Start Debugging** or simply **Run**

## vif 向けカスタマイズ by Neogenia

UI Recorder にはいくつか不具合が見つかっています。

生成された UIパスが vif で正しくWindowsSDK に付属の inspect.exe を併用してUI要素の構造を確認する必要があります。

弊社で発見した問題と、その対応状況は以下のとおりです。

- Chrome, Firefox の場合に position が付与されない<br>
  → [GitHubにissueを立てて質問中](https://github.com/microsoft/WinAppDriver/issues/1661) <br>
  原因: 子要素から親をたどるロジックになっており、兄弟要素を見ていないため、自分が何番目か分からない。<br>
  修正するには、兄弟要素を見るロジックを追加する必要がある。
  ただし vif 3.0 では、position が無くとも探索できる仕組みがあるため、本件は大きな問題になりません。
- Name属性に `]` が含まれると、正しくパスが出力されない<br>
  → [修正してGitHubにプルリクエストを投げています](https://github.com/microsoft/WinAppDriver/pull/1665)<br>
  本リポジトリでは修正をマージ済み。
- 不要なstarts-with変換が行われる場合がある<br>
  → [GitHubにissueを立てて質問中](https://github.com/microsoft/WinAppDriver/issues/1671)<br>
  [修正版はPRとして上がっています](https://github.com/neogenia-jp/WinAppDriver/pull/1/files)<br>
  しかしながらこの変換が必要と思われるシーンも見つかっており、また vif 3.0 での動作に大きな影響を与えるものではないので、マージしていません。
- UI要素は認識できるがパスから途中の階層がごっそり抜けてしまう<br>
  → 未対応
- inspect.exeではUI要素が見えているのに、UI Recorderでは認識できない要素がある<br>
  → 未対応
