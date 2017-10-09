1. Otwórz hello Android SDK Manager, klikając ikonę hello na powitania narzędzi programu Android Studio lub klikając **narzędzia** -> **Android** -> **SDK Manager**menu hello. Znajdź wersję docelową hello hello zestawu SDK systemu Android, który jest używany w projekcie, otwórz ją, klikając **Pokaż szczegóły pakietu**i wybierz polecenie **interfejsy API Google**, jeśli nie jest już zainstalowany.
2. Kliknij przycisk hello **narzędzia zestawu SDK** kartę. Jeśli usługa Google Play nie została jeszcze zainstalowana, kliknij pozycję **Google Play Services** (Usługi Google Play), jak przedstawiono poniżej. Następnie kliknij przycisk **Zastosuj** tooinstall. 
   
    Zanotuj ścieżkę zestawu SDK hello, do użycia w kolejnym kroku. 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. Otwórz hello **build.gradle** pliku w katalogu aplikacji hello.
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. Dodaj następujący wiersz w sekcji *zależności*: 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. Kliknij przycisk hello **projektu synchronizacji z plikami narzędzia Gradle** ikonę na pasku narzędzi hello.
6. Otwórz **AndroidManifest.xml** i Dodaj ten tag toohello *aplikacji* tagu.
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

