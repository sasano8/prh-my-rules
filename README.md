# 概要
textlintのルール集です。スターが多いルールをベースに、独自のルールを追加しています。


# 構成
- prh-rules: 外部リポジトリのルールです。これらのルールがベースとなります。
- prh-rules-override.yml: prh-rulesに変更を加えたい場合、ルールを追記する。※同じキーを定義すると、上書きされるように見えるが内部実装は不明。
- prh-rules.yml: 外部リポジトリのルールと衝突しない独自ルールを記述する。

# 参考サイト
- [textlint-ja](https://github.com/textlint-ja)

# 導入手順

## 新規リポジトリでルールを利用する

### 1.　サブモジュールとして追加する

``` shell
# サブモジュール（リポジトリ）を追加する
git submodule add https://github.com/sasano8/prh-my-rules prh-my-rules

# サブモジュールおよびにネストしたサブモジュールを最新にする
git submodule update --init --recursive
```

### 2.　textlintrcの設定を行う


# TODO: 試してみる
package.jsonのtextlintフィールドにパスを指定してみる。



.textlintrcを作成し、サブモジュールのルール（`prh -> rulePaths`）を追加する。

```
touch .textlintrc
```

``` json
{
  "prh": {
    "rulePaths": ["./prh-my-rules/prh-rules.yml"]
  },
  "plugins": {
    "@textlint/markdown": {
        "extensions": [".md", ".txt"]
    }
  },
  "filters": {},
  "rules": {
    "preset-ja-spacing": true,
    "spellcheck-tech-word": true,
    "preset-ja-technical-writing": true,
    "ja-technical-writing/max-kanji-continuous-len": {
        max: 8,
        allow: ["倍精度浮動小数点数"]
    },
    "ja-technical-writing/max-ten": {
        max: 4
    },
    "ja-technical-writing/max-comma": {
        max: 4
    }
  }
}
```

textlintrcフォルダに、ひな型が置いてあるので合わせて参考にしてください。

### 3.　commitする

```
git commit -m"add submodule prh-rules"
```

## ルールがすでにSubModuleとして組み込まれているリポジトリをCloneする
`git clone`実行時に、`--recursive`オプションをつけると、リポジトリ内のサブモジュールも再帰的にcloneします。

``` shell
git clone --recursive https://github.com/xxxxx/xxxxx
```

clone時に、`--recursive`を忘れてしまった場合は、次のようにサブモジュールを更新できます。

``` shell
git submodule update --recursive
```


# 基礎教養

## ら抜き言葉
