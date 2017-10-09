## <a name="create-a-device-identity"></a><span data-ttu-id="96fd7-101">Tworzenie tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="96fd7-101">Create a device identity</span></span>

<span data-ttu-id="96fd7-102">W tej sekcji można użyć narzędzia Node.js o nazwie [explorer Centrum iothub] [ iot-hub-explorer] toocreate tożsamość urządzenia w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="96fd7-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="96fd7-103">W identyfikatorach urządzeń jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="96fd7-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="96fd7-104">Uruchom następujące hello w środowisku wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="96fd7-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="96fd7-105">Następnie uruchom hello następujące polecenia toologin tooyour koncentratora.</span><span class="sxs-lookup"><span data-stu-id="96fd7-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="96fd7-106">SUBSTITUTE `{iot hub connection string}` z hello skopiowane wcześniej parametry połączenia Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="96fd7-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="96fd7-107">Na koniec utworzy nową tożsamość urządzenia o nazwie `myDeviceId` za pomocą polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="96fd7-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="96fd7-108">Zanotuj parametry połączenia urządzenia powitania od wyniku hello.</span><span class="sxs-lookup"><span data-stu-id="96fd7-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="96fd7-109">Ten ciąg połączenia urządzenia jest używany przez hello urządzenia aplikacji tooconnect tooyour Centrum IoT jako urządzenie.</span><span class="sxs-lookup"><span data-stu-id="96fd7-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="96fd7-110">Odwołuje się zbyt[wprowadzenie do korzystania z Centrum IoT] [ lnk-getstarted] tooprogrammatically tworzenia tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="96fd7-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
