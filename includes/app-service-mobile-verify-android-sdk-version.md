Z powodu bieżących prac hello wersji zestawu SDK systemu Android zainstalowane w programie Android Studio może niezgodna wersja hello w kodzie hello. Hello zestawu SDK systemu Android, do którego odwołuje się ten samouczek jest hello 23, wersja najnowszych w momencie hello zapisu. numer wersji Hello może zwiększyć jako nowe wersje hello zestawu SDK są wyświetlane, a firma Microsoft zaleca używanie hello najnowszej dostępnej wersji.

Są dwa objawy niezgodność wersji:

- Podczas tworzenia lub Odbuduj projekt hello mogą być wyświetlane komunikaty o błędach narzędzia Gradle takich jak "**nie powiodło się docelowy toofind Google Inc.:Google APIs:n**".
- Standard Android obiektów w kodzie, który powinien być rozpoznawany na podstawie `import` instrukcje generujących komunikaty o błędach.

Jeśli zostanie wyświetlona dowolna z tych, wersja hello hello zestawu SDK systemu Android zainstalowane w programie Android Studio mogą nie odpowiadać docelowy zestaw SDK hello hello pobrane projektu. Wersja hello tooverify, wprowadź następujące zmiany hello:

1. W programie Android Studio, kliknij przycisk **narzędzia** > **Android** > **SDK Manager**. Jeśli nie zainstalowano najnowszej wersji hello hello zestawu SDK platformy, kliknij przycisk tooinstall go. Zanotuj numer wersji powitania.
2. Na powitania **Eksplorator projektów** , w obszarze **skryptów narzędzia Gradle**, otwórz plik hello **build.gradle (modeule: aplikacji)**. Upewnij się, że hello **compileSdkVersion** i **buildToolsVersion** są ustawione toohello zainstalowaną najnowszą wersję zestawu SDK. tagi Hello może wyglądać następująco:

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. Hello Android Studio Project Explorer, kliknij prawym przyciskiem myszy węzeł projektu hello, wybierz **właściwości**, a w lewej kolumnie hello wybierz **Android**. Upewnij się, że hello **docelowym kompilacji projektu** ustawiono toohello tej samej wersji zestawu SDK jako hello **targetSdkVersion**.

W programie Android Studio hello pliku manifestu jest już używane toospecify hello docelowego zestawu SDK i minimalna wersja zestawu SDK, w odróżnieniu od przypadku hello Eclipse.
