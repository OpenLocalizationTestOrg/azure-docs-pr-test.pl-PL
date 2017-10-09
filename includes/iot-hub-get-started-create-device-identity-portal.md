## <a name="create-a-device-identity"></a><span data-ttu-id="f7a92-101">Tworzenie tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="f7a92-101">Create a device identity</span></span>

<span data-ttu-id="f7a92-102">W tej sekcji użyjesz hello [portalu Azure] [ lnk-azure-portal] toocreate tożsamość urządzenia w rejestrze tożsamości hello w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f7a92-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="f7a92-103">Urządzenie nie może połączyć tooIoT koncentratora, chyba że jego wpis w rejestrze tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="f7a92-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="f7a92-104">Aby uzyskać więcej informacji, zobacz część hello w "Tożsamość rejestru" hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="f7a92-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="f7a92-105">Witaj **Explorer urządzenia** w hello portalu pomaga Wygeneruj Unikatowy identyfikator urządzenia i klucz urządzenia można użyć tooidentify się podczas łączenia tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="f7a92-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="f7a92-106">W identyfikatorach urządzeń jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="f7a92-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="f7a92-107">Upewnij się, że użytkownik jest zalogowany toohello [portalu Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="f7a92-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="f7a92-108">W hello pasku dostępu kliknij **wszystkie zasoby** i Znajdź zasobu Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f7a92-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Przejdź do Centrum Iot tooyour][img-find-iothub]

1. <span data-ttu-id="f7a92-110">Po otwarciu zasobu Centrum IoT kliknij hello **Explorer urządzenia** narzędzia, a następnie kliknij przycisk **Dodaj** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="f7a92-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="f7a92-111">Podaj nazwę hello nowe urządzenie, takie jak **myDeviceId**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="f7a92-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Tworzenie tożsamości urządzenia w portalu][img-create-device]

   <span data-ttu-id="f7a92-113">Spowoduje to utworzenie nowej tożsamości urządzenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f7a92-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="f7a92-114">W hello **Explorer urządzenia**na listę urządzeń, kliknij urządzenie hello nowo utworzona i zanotuj hello **ciąg połączenia---klucz podstawowy**.</span><span class="sxs-lookup"><span data-stu-id="f7a92-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![Ciąg połączenia urządzenia][img-connection-string]

> [!NOTE]
> <span data-ttu-id="f7a92-116">Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7a92-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="f7a92-117">Urządzenia toouse identyfikatorów i klucze są przechowywane jako poświadczenia zabezpieczeń, a flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7a92-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="f7a92-118">Jeśli aplikacja wymaga toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7a92-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="f7a92-119">Więcej informacji znajduje się w temacie [IoT Hub Developer Guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera).</span><span class="sxs-lookup"><span data-stu-id="f7a92-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

