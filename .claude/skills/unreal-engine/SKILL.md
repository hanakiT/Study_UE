---

name: unreal-engine
description: Unreal Engine 5 プロジェクトの開発を支援するためのSkill。UE5のC++、Blueprint、UMG、Gameplay Framework、Editor拡張などを扱う。プロジェクト構成を確認して適切な場所にコードやアセットを追加し、Epic GamesのUnreal Engine公式コーディング規約に従って実装する。処理を追加・変更する場合は、実装前に必ず変更内容を説明してユーザーの許可を得ること。ユーザーの許可なしにコードやアセットを変更してはならない。
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Unreal Engine 5 開発ルール

## 基本方針

このSkillは、Unreal Engine 5プロジェクトの開発を支援するために使用する。

以下を常に優先する。

1. 現在のプロジェクト構成を確認してから作業する。
2. 既存の設計・命名・フォルダ構成を可能な限り尊重する。
3. Unreal Engine 5の公式仕様・公式ドキュメント・Epic Gamesのコーディング規約に従う。
4. 既存コードと重複する処理を勝手に追加しない。
5. 新しい処理を実装する前に、必ず実装内容をユーザーに説明する。
6. ユーザーから明示的な許可を得るまで、コード・Blueprint・UMG・設定ファイルなどを変更しない。
7. 不明点や設計上の判断が必要な場合は、実装する前にユーザーへ質問する。

---

# 最重要ルール：勝手に実装しない

## 実装前の確認

ユーザーから以下のような依頼を受けた場合、

* 「○○を追加して」
* 「○○できるようにして」
* 「○○を実装して」
* 「○○を修正して」
* 「Blueprintを作って」
* 「WBPを作って」
* 「C++で実装して」

すぐにファイルやコードを変更してはいけない。

まず現在のプロジェクトを調査し、実装方法を検討する。

その後、以下の形式で実装案をユーザーに提示する。

### 実装提案

* **変更するクラス**

  * `クラス名`
  * 追加・変更する処理の概要

* **追加するクラス**

  * `クラス名`
  * 親クラス
  * 役割

* **Blueprint**

  * `Blueprint名`
  * 親クラス
  * 追加する処理

* **WBP / UMG**

  * `WBP名`
  * 親クラス
  * UI構成
  * 追加する処理

* **変更するファイル**

  * `ファイルパス`
  * 変更内容

* **新しく作成するファイル**

  * `ファイルパス`
  * 役割

* **処理の流れ**

  1. ○○
  2. ○○
  3. ○○

必要に応じて、設計上の理由も簡潔に説明する。

その後、ユーザーの許可を待つ。

## 許可を得るまで実装しない

以下のようなユーザーの明示的な許可を受けるまで実装してはいけない。

* 「実装して」
* 「お願いします」
* 「それで実装して」
* 「OK」
* 「その内容で進めて」
* 「問題ない」
* 「やって」

単なる質問への回答や、実装案へのコメントだけでは実装許可とはみなさない。

例えばユーザーが、

> その方法だとどのクラスに処理を入れるの？

と質問した場合、説明だけを行い、実装してはいけない。

---

# 質問が必要な場合

実装方法を決定するために必要な情報が不足している場合は、推測して実装してはいけない。

まず質問する。

例えば、

* どのActorが処理の主体なのか不明
* 既存クラスと新規クラスのどちらに処理を入れるべきか判断できない
* BlueprintとC++のどちらを使用するか不明
* UIの表示条件が不明
* 複数の実装方法があり、要件によって適切な方法が変わる
* 既存システムとの連携方法が不明

などの場合は、必要な質問をして回答を待つ。

### 質問を優先する

「おそらくこうだろう」と推測して実装するよりも、ユーザーに確認することを優先する。

特にゲームプレイに関わる設計判断については、勝手に仕様を決めない。

---

# プロジェクト構成の確認

作業を開始する前に、現在のUnreal Engineプロジェクトの構成を確認する。

最低限、必要に応じて以下を確認する。

```text
<ProjectRoot>/
├── Config/
├── Content/
├── Source/
├── Plugins/
└── <ProjectName>.uproject
```

さらに必要に応じて、

```text
Content/
Source/
Plugins/
```

以下の既存フォルダ・モジュール・クラス構成を確認する。

## 既存構成を優先する

プロジェクトに既にフォルダ構成や命名規則が存在する場合は、それを優先する。

例えば、

```text
Content/
├── BluePrint/
├── UMG/
├── Characters/
├── Items/
├── Maps/
└── ...
```

のような構成が存在する場合、その構成を尊重する。

新しいフォルダを作る前に、既存の構成で適切な場所がないか確認する。

---

# Blueprintの配置ルール

Blueprintクラスを新しく作成する場合、原則としてプロジェクトの

```text
Content/BluePrint/
```

に追加する。

例えば、

```text
Content/
└── BluePrint/
    ├── BP_Player.uasset
    ├── BP_Enemy.uasset
    └── BP_Item.uasset
```

など。

ただし、現在のプロジェクトにBlueprint専用のサブフォルダ構成が存在する場合は、それを確認して適切な場所に配置する。

例えば、

```text
Content/BluePrint/Characters/
Content/BluePrint/Enemies/
Content/BluePrint/Items/
```

などが既に存在する場合は、クラスの役割に応じて適切な場所を選択する。

### Blueprint作成時の確認

Blueprintを作成する前に、

1. `Content/BluePrint/` の存在を確認する。
2. 既存のサブフォルダを確認する。
3. 同じ役割のBlueprintがどこに存在するか確認する。
4. 既存の命名規則を確認する。
5. 適切な配置場所を決定する。
6. 配置場所とBlueprintの役割をユーザーに提示する。
7. ユーザーの許可を得る。
8. 許可後に作成する。

---

# WBP / UMGの配置ルール

Widget Blueprint（WBP）を新しく作成する場合、原則として

```text
Content/UMG/
```

に追加する。

例えば、

```text
Content/
└── UMG/
    ├── WBP_MainMenu.uasset
    ├── WBP_MessageWindow.uasset
    └── WBP_ItemCount.uasset
```

など。

既にUI用のサブフォルダが存在する場合は、現在のプロジェクト構成に従う。

例えば、

```text
Content/UMG/Menu/
Content/UMG/HUD/
Content/UMG/Widgets/
Content/UMG/Common/
```

など。

### WBP作成時の確認

WBPを作成する前に、

1. `Content/UMG/` の存在を確認する。
2. 既存のUIフォルダ構成を確認する。
3. 同じ種類のWBPがどこに存在するか確認する。
4. 既存の命名規則を確認する。
5. 適切な配置場所を決定する。
6. 配置場所とWBPの役割をユーザーに提示する。
7. ユーザーの許可を得る。
8. 許可後に作成する。

---

# その他のアセット・クラスの配置

BlueprintやWBP以外についても、現在のプロジェクト構成を確認して適切なフォルダへ配置する。

ただし、上記は固定ルールではない。

**現在のプロジェクトに存在する構成を最優先する。**

新しいフォルダを勝手に大量作成してはいけない。

既存構成で適切な場所がない場合は、

* 新規フォルダを作る理由
* フォルダ名
* 配置するクラス・アセット
* 今後どのような用途で使用するか

をユーザーに説明し、許可を得てから作成する。

---

# C++クラスの配置

C++クラスを追加する場合は、まず現在の`Source/`構成を確認する。

例えば、

```text
Source/
└── MyProject/
    ├── Public/
    ├── Private/
    └── MyProject.Build.cs
```

のような構成の場合、Unreal Engineのモジュール構成に従って配置する。

プロジェクトに既存のカテゴリ別フォルダがある場合は、それを利用する。

例：

```text
Source/MyProject/Public/Characters/
Source/MyProject/Public/Components/
Source/MyProject/Public/Interfaces/
Source/MyProject/Public/Systems/
```

など。

既存構成を確認せずに新しいフォルダを作成してはいけない。

---

# C++の基本ルール

C++コードはEpic GamesのUnreal Engine公式Coding Standardに従う。

特に以下を遵守する。

## 命名規則

Unreal Engineの命名規則を使用する。

例：

```cpp
UCLASS()
class MYPROJECT_API UMyComponent : public UActorComponent
{
    GENERATED_BODY()
};
```

```cpp
class AMyActor : public AActor
{
    GENERATED_BODY()
};
```

```cpp
struct FMyData
{
};
```

```cpp
enum class EMyState : uint8
{
    None,
    Active,
};
```

Unreal Engineの型プレフィックスを適切に使用する。

* `U` : `UObject`派生クラス
* `A` : `AActor`派生クラス
* `F` : 構造体
* `E` : 列挙型
* `T` : テンプレート
* `S` : Slate Widget

変数・関数・クラス名は、役割が明確になる名前を使用する。

---

# UEの型を優先する

Unreal Engineでは、状況に応じてUEの型・コンテナを使用する。

例：

```cpp
FString
FName
FText
FVector
FRotator
FTransform
TArray
TMap
TSet
TObjectPtr
TWeakObjectPtr
```

整数型についても必要に応じて、

```cpp
int32
uint32
int64
uint64
uint8
```

などUnreal Engineの型を使用する。

---

# UObject / Actorの扱い

Unreal EngineのGCおよびObject Ownershipを尊重する。

UObject派生オブジェクトについては、適切な参照方法を使用する。

例えば、必要に応じて、

```cpp
UPROPERTY()
TObjectPtr<UMyObject> MyObject;
```

などを使用する。

生のポインタを不用意に所有目的で使用しない。

---

# UPROPERTY / UFUNCTION

Reflection Systemを使用するクラスでは、必要に応じて適切なUnreal Engine Macroを使用する。

例：

```cpp
UPROPERTY(EditAnywhere, BlueprintReadOnly)
float Health;
```

```cpp
UFUNCTION(BlueprintCallable)
void StartInteraction();
```

ただし、Blueprint公開が本当に必要かを確認する。

「とりあえず全部BlueprintCallableにする」といった実装は行わない。

---

# Includeルール

必要なHeaderを明示的にIncludeする。

別のHeaderから間接的にIncludeされることを前提にしない。

可能な場合はForward Declarationを利用し、不要な依存関係を増やさない。

例：

```cpp
class UMyComponent;
class AMyActor;
```

Headerで完全な型定義が必要な場合のみ適切なHeaderをIncludeする。

---

# Build.cs

新しいModule依存関係が必要になった場合は、`Build.cs`を確認する。

例えば、

```cpp
PublicDependencyModuleNames
```

や

```cpp
PrivateDependencyModuleNames
```

を適切に使用する。

不要なModule依存を追加しない。

Build.csを変更する場合も、実装前に変更内容をユーザーへ提示して許可を得る。

---

# C++コードのフォーマット

Epic GamesのUnreal Engine Coding Standardに従う。

例えば、波括弧は新しい行に配置する。

```cpp
if (bIsActive)
{
    DoSomething();
}
```

1行だけの処理であっても、原則として波括弧を省略しない。

```cpp
// Good
if (bIsValid)
{
    return;
}
```

以下のような書き方は避ける。

```cpp
// Avoid
if (bIsValid) return;
```

関数やクラスは責務を明確にし、巨大な関数を作らない。

必要に応じて処理を適切な関数・クラスへ分割する。

---

# Blueprintの実装方針

Blueprintを作成・変更する場合も、C++と同様に既存プロジェクトの設計方針を尊重する。

特に、

* Actor
* ActorComponent
* Character
* Controller
* GameMode
* GameState
* PlayerState
* PlayerController
* GameInstance
* Subsystem
* Widget
* WidgetComponent

など、どのクラスが処理を担当すべきかを確認する。

処理をBlueprintに追加する前に、

> 「なぜこのBlueprintにこの処理を追加するのか」

を説明できる状態にする。

---

# BlueprintとC++の役割分担

BlueprintとC++のどちらで実装するか迷う場合は、勝手に決定しない。

プロジェクトの既存構成を確認したうえで、候補を提示する。

例えば、

### 案A：C++側に処理を追加

* ロジックをC++で管理
* Blueprintは設定・表示・イベント接続を担当

### 案B：Blueprint側に処理を追加

* 処理が比較的単純
* デザイナーがEditor上で変更する可能性がある

のように比較し、必要であればユーザーに確認する。

---

# UMG / Widget

WBPを作成・変更する場合は、

* Widget Tree
* Designer
* Event Graph
* Widget Blueprintの親クラス
* UIロジック
* データの取得元
* 表示・非表示条件

を確認する。

UIのロジックをWBPだけに詰め込みすぎない。

ゲームロジックとUI表示ロジックを適切に分離する。

---

# 既存コードを尊重する

既存のコードを変更する場合、変更前に周辺コードを確認する。

特に、

* 継承関係
* Component構成
* Interface
* Delegate
* Event
* Subsystem
* GameInstance
* GameMode
* GameState
* PlayerController
* PlayerState
* Data Asset
* Data Table

などの関連箇所を確認する。

既存処理と同じ目的の処理を新しく作らない。

既存処理を再利用できる場合は、再利用を優先する。

---

# 変更範囲を最小限にする

ユーザーから指定されていない箇所を勝手にリファクタリングしない。

例えば、

> 「この機能を追加して」

という依頼に対して、

* 無関係なクラスのリファクタリング
* 命名規則の一括変更
* フォルダ構成の変更
* 不要なコメントの大量追加
* 無関係なコードの整理

などを行ってはいけない。

必要な変更だけを行う。

---

# エラー修正時のルール

コンパイルエラーやBlueprintエラーを修正する場合も、原因を確認してから変更する。

以下の順番を基本とする。

1. エラー内容を確認する。
2. 該当箇所を確認する。
3. 関連するクラス・Module・依存関係を確認する。
4. 原因を特定する。
5. 修正案をユーザーへ提示する。
6. ユーザーの許可を得る。
7. 修正する。
8. 必要に応じてBuild・Compile・検証を行う。

単にエラーが出たからといって、関係しそうなコードを無差別に変更しない。

---

# 実装後の報告

ユーザーの許可を得て実装した後は、以下を報告する。

## 変更内容

* 変更したクラス
* 追加したクラス
* 追加・変更したBlueprint
* 追加・変更したWBP
* 変更したファイル
* 主な処理

## 配置場所

例えば、

```text
Content/BluePrint/BP_Item.uasset
Content/UMG/WBP_ItemCount.uasset
Source/MyProject/Private/Items/Item.cpp
```

のように明示する。

## 検証結果

可能であれば、

* Compile
* Build
* UnrealHeaderTool
* Blueprint Compile
* Automated Test
* Packaging

などの結果を報告する。

実行していない検証について「成功した」と報告してはいけない。

---

# Unreal Engine公式ドキュメントを優先する

Unreal Engineの仕様について判断する場合、可能な限りEpic Games公式ドキュメントを優先する。

特に以下については公式ドキュメントを優先する。

* C++ Coding Standard
* Gameplay Framework
* UObject
* Actor
* Components
* Reflection System
* UPROPERTY
* UFUNCTION
* Blueprint
* UMG
* Slate
* Gameplay Ability System
* Unreal Build Tool
* Module
* Editor API

UEのバージョンによって仕様が異なる可能性がある場合は、**現在のプロジェクトのUnreal Engineバージョンを確認してから判断する。**

---

# 最終原則

このSkillで最も重要なのは以下のルールである。

1. **まずプロジェクトを確認する。**
2. **既存の構成・設計を尊重する。**
3. **Blueprintは原則 `Content/BluePrint/` に配置する。**
4. **WBPは原則 `Content/UMG/` に配置する。**
5. **その他のクラス・アセットは現在のプロジェクト構成を確認して適切な場所に配置する。**
6. **処理を追加・変更する場合、最初に「どのクラスに、どの処理を追加するのか」を説明する。**
7. **ユーザーの許可を得るまで実装しない。**
8. **不明点がある場合は、推測せず先に質問する。**
9. **勝手に仕様を決めない。**
10. **Epic GamesのUnreal Engine公式Coding Standardに従う。**
11. **ユーザーが指定していない無関係なコードを変更しない。**
12. **実際に行っていない検証結果を報告しない。**
