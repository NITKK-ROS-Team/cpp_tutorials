# Getting start
Visual Studioで新規プロジェクトを作成してC言語で記載されたプログラムを実行します。

## Create a New Project

1. `新しいプロジェクトの作成`を選択します。

    ![new_prj](./images/01_new_prj.png)

2. `空のプロジェクト`を選択し`次へ`をクリックします。

    ![emp_prj](./images/02_empty_prj.png)

3.  プロジェクト名などはデフォルトのままで問題ありません。

    ![def](./images/03_def.png)

## Build

1. `ソリューションエクスプローラ`にある`ソースファイル`フォルダを右クリックします。

    ![sln](./images/04_src_file.png)

2. 追加 -> 新しい項目の順に選択します。

    ![new](./images/05_main_cpp.png)

3. C++ファイルを選択し追加します。この時にファイル名を`main.cpp`に変更します。

    ![maincpp](./images/06_add_file.png)

4. `main.cpp`に以下のプログラムを記入します。

    ```C
    #include <stdio.h>

    int main(void) {
        printf("HelloWorld");
        return 0;
    }
    ```

5. `ローカルWindowsデバッガー`をクリックして実行します。`arm64`と記載されている部分は環境によって異なります。

    ![final](./images/07_build.png)

6. 黒い画面が起動し`HelloWorld`と表示されれば成功です。

    ![comp](./images/07_comp.png)