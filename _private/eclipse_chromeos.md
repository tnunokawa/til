
    ChromeBookにjava11とeclipseを入れる
    =============================

    <section>
        ラップトップChromeBookしか持ってないけどコメダ珈琲でJava SE11 Silverの勉強したい！ということで入れてみました。モノ好きな方はご一読を....。
        ChromeBookのスペック↓
        HP ChromeBook x360 14-da0008TU
        130.0.6723.79 (Official Build) beta （64 ビット）


        ChromeBookでLinux開発環境を有効化
        ------------------------

        ChromeBookにeclipsをインストールする前に、ネイティブLinuxアプリのサポートを有効にする必要があります。
        設定を開く（Chromebook右下 時計 → 歯車アイコン）
        サイドバー「ChromeOSについて」→「Linux開発環境」
        Linuxサポートをオンにする
        画面の指示に従ってLinux環境を設定する（デフォルト設定でOK）
        Linux環境では日本語の入力、キー配列などに関して設定が必要な場合があります。お好みでやりましょう。


        Java 11をインストール
        --------------

        すでにJavaが入っているor11以外を入れるつもりの方は飛ばしてください。
        <!-- 太字 -->**Javaがインストールされていないことを確認**


            $ java -version
            -bash: java: コマンドが見つかりません

        		私の環境ではaptでJava11を入れることができなかったためAdoptiumを使用します。


        		少々めんどくさいです。



        		↓からJava11のバイナリをダウンロード(Adoptium)

        https://adoptium.net/temurin/releases/?version=11&os=linux&arch=x64&package=jdk


        <!-- 画像を挿入 -->  

        ![adoptium](Adoptium.png)



        		filterを画像のように設定し.tar.gzをクリック



        		Adoptiumとは



        > 			"Eclipse
        > 			Adoptium（エクリプス・アドプティウム）は、信頼性が高く、オープンソースのJavaランタイム（JDK）を提供するプロジェクトです。Adoptiumは、以前のAdoptOpenJDKがEclipse
        > 			Foundationに移管され、名前が変更されたプロジェクトであり、Java開発者に無料で安定したJavaディストリビューションを提供することを目的としています。"
        > 			  
        >
        >
        > <cite>by ChatGPT</cite>  
        <span class="marker">OpenJDK11U-jdk_x64_linux_hotspot_11.0.25_9.tar.gz</span>


        		こんな感じのがダウンロードできると思います。この記事で出てくるコマンドのファイル名などはご自身がダウンロードしたものにしたがって適宜修正してください。


        		ダウンロードした.tar.gzファイルをLinuxに移動します。私は~/tmp/というディレクトリを作ってそこに移動しました。



        		.tar.gzファイルを解凍し/opt/に移動します。


        		解凍



            $ tar -xzf OpenJDK11U-jdk_x64_linux_hotspot_11.0.25_9.tar.gz

        		移動



            $ sudo mv jdk-11.0.25+9 /opt/

        		環境変数を設定します。



            $ echo 'export JAVA_HOME=/opt/jdk-11.0.25+9' >> ~/.bashrc
            $ echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
            $ source ~/.bashrc

        		Javaが入ったか確認



            $ java -version
            openjdk version "11.0.25" 2024-10-15
            OpenJDK Runtime Environment Temurin-11.0.25+9 (build 11.0.25+9)
            OpenJDK 64-Bit Server VM Temurin-11.0.25+9 (build 11.0.25+9, mixed mode)

        		このように出力されれば成功です。



        Eclipseをインストール
        --------------
        		deb版(インストーラみたいなやつ)がないので↓からバイナリをダウンロードします。

        https://www.eclipse.org/downloads/packages/release/2024-09/r


        <span class="marker">eclipse-committers-2024-09-R-linux-gtk-x86_64.tar.gz</span>


        		こんな感じのやつをダウンロードしてきましょう。


        		ダウンロードした.tar.gzファイルをLinux(~/tmp/)に移動します。



        		解凍し/opt/に移動します。


        		解凍



            $ tar -xzf eclipse-committers-2024-09-R-linux-gtk-x86_64.tar.gz

        		移動



            $ sudo mv eclipse /opt/

        		このままでは起動できないので、userのパスが通っているところにシンボリックリンクを作成します。



            sudo ln -s /opt/eclipse/eclipse /usr/local/bin/

        		Eclipseを起動



            $ eclipse

        		Eclipseが起動できれば成功です。


        		ChromeBookでは重くて使い物にならない噂もあるらしいです。(私の環境では今の所少し重いかな？くらいです。)



        +α Eclipseを日本語化
        ---------------
        		↑で起動したEclipseは英語になっているかと思います


        		Eclipseが英語のままだと困る方はEclipseの日本語化プラグインであるPleiadesを入れましょう。



        		↓からPleiadesをダウンロード

        https://willbrains.jp/


        <span class="marker">pleiades.zip</span>



        		ダウンロードした.zipファイルをLinuxに移動→/opt/eclipse/に解凍



            $ cd /opt/eclipse/
            $ unzip ~/tmp/pleiades.zip


        		eclipse.iniの最後に
        		<span class="marker">-javaagent:/opt/eclipse/plugins/jp.sourceforge.mergedoc.pleiades/pleiades.jar</span>を追記してプラグインを読み込みましょう。



        		Eclipseを起動して日本語化を確認



            $ eclipse


        +α Eclipseをアイコンクリックで起動できるようにする
        ------------------------------
        		アイコンから起動できるとなんかいいですよね。


        		ChromeBookでは<span class="marker">/usr/share/applications/</span>に.desktopファイルを作成したものがランチャーなどに現れるようです。



        		まずEclipseのアイコン画像を用意しましょう(.pngなど)。


        		Eclipse起動スクリプトを作成。私はlaunch_eclipse.shを作成しました。



            #!/bin/bash
            eclipse

        		起動スクリプトを実行可能に設定



            $ chmod +x launch_eclipse.sh

        		/usr/share/applications/にeclipse.desktopを作成



            [Desktop Entry]
            Name=Eclipse
            Comment=Eclipse
            Exec=起動スクリプト(launch_eclipse.sh)のpath
            Icon=アイコン画像のpath
            Terminal=false
            Type=Application
            Categories=Unknown

        		これでランチャーに追加されたアイコンをクリックするとEclipseが起動するようになったかと思います。



        +α Eclipseでgithub copilotを有効化
        -----------------------------
        		マーケットプレイスでCopilot4Eclipseを検索しインストールします。


        		右下のCopilot4Eclipseのアイコンをクリック→Sign In to GitHub Copilotを選択しアカウント認証へ進みます。


        		デバイスコードと認証URLが書かれたポップアップが出てくるので、URLをコピーしておきます。


        		ポップアップのOKか、Copy Code and Openを押すと何やらカウントダウンが始まります(本来であればブラウザで認証画面が開くが私の環境では開かなかった)


        		その隙にコピーしたurlをブラウザに貼り付け、画面に従って認証番号を入力


        		完了！

    </section>
