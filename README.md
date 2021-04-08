# vuetify-project

## iconの表示
マテリアルデザインアイコンのライブラリをインストール
```
npm install --save @mdi/font
```
`main.js` に `@mdi/font` インポートを記述
```
import '@mdi/font/css/materialdesignicons.css'
```

## エンターキーでの追加
- `v-card`タグ内にsubmitイベントを抑える
- `v-text-field`内に`@keyup.enter="Method"`を追加  
  `Method`の部分を`v-btn`と同じメソッドにすれば、ボタンを押したときと同じ挙動になる。
```
</v-app-bar>
      <v-card class="mx-auto" outlined max-width="1200" @submit.prevent>
        <v-card-title>
          <v-text-field label="入力欄" placeholder="ToDoの入力" outlined v-model="task" @keyup.enter="add()"></v-text-field>
```          