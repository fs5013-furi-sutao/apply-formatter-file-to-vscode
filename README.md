# VSCode にフォーマッタのファイルを適用する

## フォーマッター定義ファイルの作成

VSCodeでJavaのフォーマッターを指定する箇所があるのですが、URLまたはローカルファイルパスが指定できます。今回はカスタマイズしたいので、まずは独自のフォーマッターを作成します。定義ファイルをテキストファイルなどで作成もできるのですが、GUI上のほうがプレビューなどもあるので、今回はEclipseを使います。

1. Eclipseを起動し、[Preferences]を開きます。
2. [Java]-[Code Style]-[Formatter]を選択します。
3. [New]ボタンをクリックします。
4. [Profile name]に任意の名前（ここでは「MyFormatter」）を入力し、「OK」ボタンをクリックします。
5. 以下のフォーマット設定を行います。　　

|カテゴリ	|項目	|値 |
|:-- |:-- |:-- |
|Indentation	|Tab policy	|spaces only |
|Line Wrapping	|Never join already wrapped lines	|チェック |

6. 設定が完了したら、「OK」ボタンをクリックします。
7. [Active Profile]から上記で作成したもの（MyFormatter）を選択し、[Export All]ボタンをクリックし、ローカルに保存します。保存するファイル名は「formatter.xml」としておきます。

## 設定値の概要

- Tab policy: spaces only
タブ使用時に、スペースに変換します。

- Never join already wrapped lines: チェック
改行済みのコードはフォーマットされません。これがないと、１行の最大サイズの範囲内で、改行されたコードが結合されて（改行が削除されて）しまいます。

## VSCodeの設定

[Settings]を開き、以下の設定を行います。

|項目	|設定値 |
|:-- |:-- |
|Editor: Detect Indentation	チェックなし |
|Editor: Format On Save	|チェック |
|Java › Format › Settings: Url	|/path/to/formatter.xml |
|Java › Format › Settings: Profile	|MyFormatter |
|Java › Save Actions: Organize Imports	|チェック |

## 設定値の概要

- Editor: Detect Indentation
インデントの扱い（タブをスペースにするとか、いくつインデントするとかなど）をファイルごとに設定可能にするかの設定です。チェックがない場合はフォーマット定義に従います。

- Editor: Format On Save
保存時にフォーマットが自動で実行されます。

- Java › Format › Settings: Url
フォーマット定義ファイルを指定します。ここで定義されたフォーマットが実行されます。

- Java › Format › Settings: Profile
フォーマット定義ファイルに設定したプロファイル名です。どのプロファイルを適用するか設定します。

- Java › Save Actions: Organize Imports
保存時にインポートの最適化が実行されます。未使用のインポート削除、インポートのソートが実行されます。

## setting.json の記載例

``` json
{
    "editor.formatOnSave": true,
    "java.format.settings.url": "C:\\formatter\\java-boot-camp-style.xml",
    "java.format.enabled": true,
    "java.format.settings.profile": "Java Bootcamp Style",
    "window.zoomLevel": 2
}
```

## フォーマッタの XML ファイルの例

このリポジトリの以下の XML ファイルを参考にしてください

java-boot-camp-style.xml
https://github.com/fs5013-furi-sutao/apply-formatter-file-to-vscode/blob/main/java-boot-camp-style.xml
