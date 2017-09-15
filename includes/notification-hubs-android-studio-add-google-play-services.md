1. <span data-ttu-id="17029-101">Otwórz narzędzie Android SDK Manager, klikając ikonę na pasku narzędzi programu Android Studio lub klikając kolejno opcje **Tools** (Narzędzia) -> **Android** -> **SDK Manager** w menu.</span><span class="sxs-lookup"><span data-stu-id="17029-101">Open the Android SDK Manager by clicking the icon on the toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on the menu.</span></span> <span data-ttu-id="17029-102">Znajdź wersję docelową zestawu SDK systemu Android używaną w projekcie, otwórz ją, klikając opcję **Show Package Details** (Pokaż szczegóły pakietu), po czym wybierz opcję **Google APIs** (Interfejsy API Google), jeśli nie została ona jeszcze zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="17029-102">Locate the target version of the Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="17029-103">Kliknij kartę **SDK Tools** (Narzędzia zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="17029-103">Click the **SDK Tools** tab.</span></span> <span data-ttu-id="17029-104">Jeśli usługa Google Play nie została jeszcze zainstalowana, kliknij pozycję **Google Play Services** (Usługi Google Play), jak przedstawiono poniżej.</span><span class="sxs-lookup"><span data-stu-id="17029-104">If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="17029-105">Następnie kliknij opcję **Apply** (Zastosuj), aby zainstalować usługę.</span><span class="sxs-lookup"><span data-stu-id="17029-105">Then click **Apply** to install.</span></span> 
   
    <span data-ttu-id="17029-106">Zanotuj ścieżkę zestawu SDK, która będzie potrzebna w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="17029-106">Note the SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="17029-107">Otwórz plik **build.gradle** w katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="17029-107">Open the **build.gradle** file in the app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="17029-108">Dodaj następujący wiersz w sekcji *zależności*:</span><span class="sxs-lookup"><span data-stu-id="17029-108">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="17029-109">Kliknij ikonę **Sync Project with Gradle Files** (Synchronizuj projekt z plikami narzędzia Gradle) na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="17029-109">Click the **Sync Project with Gradle Files** icon in the tool bar.</span></span>
6. <span data-ttu-id="17029-110">Otwórz plik **AndroidManifest.xml** i dodaj ten tag do tagu *aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="17029-110">Open **AndroidManifest.xml** and add this tag to the *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

