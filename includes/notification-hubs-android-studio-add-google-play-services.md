1. <span data-ttu-id="cf5bd-101">Otwórz hello Android SDK Manager, klikając ikonę hello na powitania narzędzi programu Android Studio lub klikając **narzędzia** -> **Android** -> **SDK Manager**menu hello.</span><span class="sxs-lookup"><span data-stu-id="cf5bd-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="cf5bd-102">Znajdź wersję docelową hello hello zestawu SDK systemu Android, który jest używany w projekcie, otwórz ją, klikając **Pokaż szczegóły pakietu**i wybierz polecenie **interfejsy API Google**, jeśli nie jest już zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="cf5bd-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="cf5bd-103">Kliknij przycisk hello **narzędzia zestawu SDK** kartę. Jeśli usługa Google Play nie została jeszcze zainstalowana, kliknij pozycję **Google Play Services** (Usługi Google Play), jak przedstawiono poniżej.</span><span class="sxs-lookup"><span data-stu-id="cf5bd-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="cf5bd-104">Następnie kliknij przycisk **Zastosuj** tooinstall.</span><span class="sxs-lookup"><span data-stu-id="cf5bd-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="cf5bd-105">Zanotuj ścieżkę zestawu SDK hello, do użycia w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="cf5bd-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="cf5bd-106">Otwórz hello **build.gradle** pliku w katalogu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cf5bd-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="cf5bd-107">Dodaj następujący wiersz w sekcji *zależności*:</span><span class="sxs-lookup"><span data-stu-id="cf5bd-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="cf5bd-108">Kliknij przycisk hello **projektu synchronizacji z plikami narzędzia Gradle** ikonę na pasku narzędzi hello.</span><span class="sxs-lookup"><span data-stu-id="cf5bd-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="cf5bd-109">Otwórz **AndroidManifest.xml** i Dodaj ten tag toohello *aplikacji* tagu.</span><span class="sxs-lookup"><span data-stu-id="cf5bd-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

