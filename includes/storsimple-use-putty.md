<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="63909-101">tooconnect za pośrednictwem konsoli szeregowej hello</span><span class="sxs-lookup"><span data-stu-id="63909-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="63909-102">Podłącz kabel szeregowy urządzenie toohello, (bezpośrednio lub za pośrednictwem adaptera szeregowego USB).</span><span class="sxs-lookup"><span data-stu-id="63909-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="63909-103">Otwórz hello **Panelu sterowania**, a następnie otwórz hello **Menedżera urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="63909-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="63909-104">Zidentyfikuj port hello COM pokazane na następującej ilustracji hello.</span><span class="sxs-lookup"><span data-stu-id="63909-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![Łączenie za pośrednictwem konsoli szeregowej](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="63909-106">Uruchom program PuTTY.</span><span class="sxs-lookup"><span data-stu-id="63909-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="63909-107">W okienku po prawej stronie powitania, zmień hello **typ połączenia** za**Serial**.</span><span class="sxs-lookup"><span data-stu-id="63909-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="63909-108">W okienku po prawej stronie powitania wpisz odpowiedni port COM. hello.</span><span class="sxs-lookup"><span data-stu-id="63909-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="63909-109">Upewnij się, że parametry konfiguracji portu hello są ustawione w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="63909-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="63909-110">Szybkość: 115 200</span><span class="sxs-lookup"><span data-stu-id="63909-110">Speed: 115,200</span></span>
   * <span data-ttu-id="63909-111">Bity danych: 8</span><span class="sxs-lookup"><span data-stu-id="63909-111">Data bits: 8</span></span>
   * <span data-ttu-id="63909-112">Bity stopu: 1</span><span class="sxs-lookup"><span data-stu-id="63909-112">Stop bits: 1</span></span>
   * <span data-ttu-id="63909-113">Parzystość: Brak</span><span class="sxs-lookup"><span data-stu-id="63909-113">Parity: None</span></span>
   * <span data-ttu-id="63909-114">Sterowanie przepływem: Brak</span><span class="sxs-lookup"><span data-stu-id="63909-114">Flow control: None</span></span>
     
     <span data-ttu-id="63909-115">Te ustawienia zostały pokazane hello następującej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="63909-115">These settings are shown in hello following illustration.</span></span>
     
     ![Ustawienia programu PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="63909-117">Jeśli hello domyślne ustawienie sterowania przepływem nie działa, spróbuj hello przepływu sterowania tooXON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="63909-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="63909-118">Kliknij przycisk **Otwórz** toostart sesję serial.</span><span class="sxs-lookup"><span data-stu-id="63909-118">Click **Open** toostart a serial session.</span></span>

