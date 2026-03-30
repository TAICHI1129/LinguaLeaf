# LinguaLeaf
言語学習アプリケーション

**LinguaLeaf** は、言語学習コースをオンラインで公開・学習できる  Webアプリケーション プロジェクトです。 

URL: https://lingualeaf.ct.ws/

GitHub Pages版: https://taichi1129.github.io/LinguaLeaf/

## コースの作り方
LLC(Learn Language Course)ファイルを使用します。

拡張子は.llcですが、.jsonでも正常に動作します。

中身はJSON構文です。

TokFormatという簡単な言語からJSONへ[変換](https://lingualeaf.ct.ws/TokFormat_to_LLC.html)することができます。

JSONでの記述については[guide.md](guide.md)を参照してください。

例:
`````LLC
{
  "id": "my_course_01",
  "name": "コース名",
  "icon": "🇫🇷",
  "description": "説明文",
  "lessons": [
    {
      "id": "lesson_1",
      "title": "レッスン1",
      "type": "fill",
      "questions": [
        {
          "type": "fill",
          "question": "問題文",
          "options": ["選択肢A","選択肢B","選択肢C","選択肢D"],
          "answer": 0,
          "explanation": "解説（任意）"
        }
      ]
    }
  ]
}
`````


## 📄 ライセンス

MIT License  
詳細は [LICENSE](LICENSE) を参照してください。
