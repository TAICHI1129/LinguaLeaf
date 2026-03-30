# LinguaLeaf コース制作ガイド（製作者向け）

## 1. 概要

LinguaLeafでは、コースは **LLC形式** で作成します。
コースは「レッスン」と「問題」で構成されます。

---

## 2. 基本構造

```json
{
  "id": "course_id",
  "name": "コース名",
  "icon": "📘",
  "description": "説明文",
  "lessons": []
}
```

### 必須項目

| 項目      | 説明           |
| ------- | ------------ |
| id      | コース識別子（重複不可） |
| name    | コース名         |
| lessons | レッスンの配列      |

---

## 3. レッスン構造

```json
{
  "id": "lesson_id",
  "title": "レッスン名",
  "type": "fill",
  "questions": []
}
```

### 項目

| 項目        | 説明        |
| --------- | --------- |
| id        | レッスンID    |
| title     | 表示名       |
| type      | 問題タイプ（任意） |
| questions | 問題一覧      |

---

## 4. 問題タイプ

### 4.1 選択問題（fill）

```json
{
  "type": "fill",
  "question": "問題文",
  "options": ["A","B","C","D"],
  "answer": 0,
  "explanation": "解説（任意）"
}
```

* `answer` は **配列のインデックス** を指定します。
* `options` は必須項目です。

---

### 4.2 タイピング問題（typing）

```json
{
  "type": "typing",
  "question": "問題文",
  "answer": ["hello","Hello"],
  "hint": "ヒント（任意）"
}
```

* `answer` は文字列または文字列配列を指定します。
* 大文字・小文字は無視されます。

---

### 4.3 リスニング問題（listening）

```json
{
  "type": "listening",
  "question": "音声を聞いて答えてください",
  "audio_url": "https://example.com/audio.mp3",
  "audio_text": "Hello",
  "lang": "en-US",
  "options": ["Hello","Bye"],
  "answer": 0
}
```

#### 音声仕様

優先順位は以下の通りです：

1. `audio_url`
2. `audio_text`（TTSを使用）

### 4.4 カード問題(cards)

```json
{
  "type": "cards",
  "question": "カードを並べて文を完成させてください",
  "word_bank": ["I", "am", "a", "student"],
  "answer": ["I", "am", "a", "student"],
  "explanation": "主語 + be動詞 + 冠詞 + 名詞"
}
```
* word_bank: 選択カード一覧
* answer: 正しい並び順（完全一致で正解判定）

---

## 5. ファイル仕様

| 項目    | 内容              |
| ----- | --------------- |
| 拡張子   | .llc または .json  |
| 文字コード | UTF-8           |
| 形式    | JSON（コメントは使用不可） |

---

## 6. エラー要因（注意）

制作時によく発生するエラー例は以下の通りです：

* JSON構文エラー（カンマの付け忘れなど）
* `id` 未設定
* `lessons` が配列ではない
* `answer` が範囲外
* `options` が不足している

---

## 7. 設計ガイドライン

### 良いコース

* 難易度が段階的に設定されている
* 複数の問題タイプを組み合わせている
* 解説が含まれている

### 避けるべきコース

* 初回から難易度が高すぎる
* すべて同じ形式の問題で構成されている
* 解説がない

---

## 8. ベストプラクティス

* `id` は一意にする（例: `en_basic_01`）
* レッスンは小分けにして3〜5問程度にする
* タイピング問題は複数回答を許可する
* リスニング問題にはTTSフォールバックを用意する

---

## 9. サンプル

```json
{
  "id": "en_basic",
  "name": "英語基礎",
  "icon": "🇬🇧",
  "description": "英語の基本",
  "lessons": [
    {
      "id": "greeting",
      "title": "挨拶",
      "questions": [
        {
          "type": "fill",
          "question": "Helloの意味は？",
          "options": ["こんにちは","さようなら"],
          "answer": 0
        },
        {
          "type": "typing",
          "question": "「ありがとう」を英語で入力してください",
          "answer": ["thank you","Thanks"]
        }
      ]
    }
  ]
}
```

---

## 10. 配布方法

* ファイルとして配布（.llc）
* URL配布（CORS許可が必要です）

---

## 11. まとめ

* コースはJSON形式のデータで構成されます。
* 指定の構造に従えば正しく動作します。
* 設計次第でコースの品質が決まります。
