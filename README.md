# Servlet/JSP 演習問題

## 第1章 HTTPリクエスト

### 演習1-1

フルーツのチェックボックスを用意し、チェックされたフルーツを次の画面で表示する。


**fruits-list.html**

<img src="images/01-01.png" alt="演習1" width="800">

**FruitsListServlet.java** （パッケージ：jp.sample.servlet、@WebServlet：fruitslist）

<img src="images/01-02.png" alt="演習1" width="800">

[解答例](/answer/01-01.md)

<br>

### 演習1-2

メールアドレスとパスワードの入力ボックスを用意する。

・メールアドレスが「test@sample.jp」、パスワードが「pass01」の場合、「Login success」と表示<br>
・上記以外の場合、「Login failure」と表示


**login.html**

<img src="images/01-03.png" alt="演習1" width="800">

**LoginSampleServlet.java** （パッケージ：jp.sample.servlet、@WebServlet：loginsample）

<img src="images/01-04.png" alt="演習1" width="800">

<img src="images/01-05.png" alt="演習1" width="800">

[解答例](/answer/01-02.md)

<br>
<hr>

## 第2章 HTTPレスポンス

### 演習2-1

ログイン時の表示内容を以下のように変更する。<br>
・タイトル：Login<br>
・ログイン成功時：h1タグで「ログイン成功」と表示<br>
・ログイン失敗時：h2タグで「ログイン失敗」と表示<br>

<br>

**LoginSampleServlet.java** （パッケージ：jp.sample.servlet、@WebServlet：loginsample）

<img src="images/02-01.png" alt="演習1" width="800">

<img src="images/02-02.png" alt="演習1" width="800">

[解答例](/answer/02-01.md)

<br>
<hr>

## 第3章 リクエストのフォワード

### 演習3-1

ログイン時の表示方法を以下のように変更する。<br>
・ログイン成功時：スケジュール一覧を表示するScheduleServletへフォワードする<br>
・ログイン失敗時：ログイン画面へフォワードする<br>

<br>

**Schedule.java** （パッケージ：jp.sample.dto）

**フィールド**

|型|フィールド名|
|--|----------|
|int|ID|
|String|日時|
|String|タイトル|
|String|場所|

**コンストラクタ**

|引数|内容|
|---|----|
|ID、日時、タイトル、場所|引数の各値をフィールドに代入する|

**メソッド**

※各フィールドのsetter/getterを作成する

<br>

**ScheduleServlet.java** （パッケージ：jp.sample.servlet、@WebServlet：loginsample）

<img src="images/03-01.png" alt="演習1" width="800">

```java
package jp.sample.servlet;

import java.io.IOException;
import java.util.Arrays;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import jp.sample.dto.Schedule;

/**
 * Servlet implementation class ScheduleServlet
 */
@WebServlet("/schedule")
public class ScheduleServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    /**
     * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
     */
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        List<Schedule> scheduleList = Arrays.asList(new Schedule(1, "20xx-06-10 13:00", "〇〇さんとランチ", "梅田"),
                            new Schedule(1, "20xx-06-11 10:00", "ミーティング", "本社会議室"),
                            new Schedule(1, "20xx-06-13 19:00", "飲み会", "焼き鳥烏丸"));

        // TODO
    }
}
```

[解答例](/answer/03-01.md)

<br>

### 演習3-2

URL「~/(プロジェクト名)/loginsample」に直接アクセスした場合、ログイン画面が表示されるように修正する。

[解答例](/answer/03-02.md)

<br>
<hr>


## 第4章 レスポンスのリダイレクト

### 演習4-1

POSTでログインし、スケジュール画面（ScheduleServlet）へフォワードしたが、画面を再読み込みするとPOST送信でログイン処理が再度実行されてしまう。<br>
そこで、ログイン成功時のScheduleServletへのフォワードを、ScheduleServletへの**リダイレクト**に修正する。

[解答例](/answer/04-01.md)
