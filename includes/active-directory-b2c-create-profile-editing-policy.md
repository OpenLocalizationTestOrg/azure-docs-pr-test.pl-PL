<span data-ttu-id="ea72c-101">Profil tooenable edycji w swojej aplikacji, konieczne będzie toocreate profilu edytowanie zasad.</span><span class="sxs-lookup"><span data-stu-id="ea72c-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="ea72c-102">Ta zasada opisuje hello procesów, które konsumentów będzie przejście przez podczas edycji i hello zawartość profilu tokenów otrzymujących aplikacji hello na pomyślne zakończenie.</span><span class="sxs-lookup"><span data-stu-id="ea72c-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="ea72c-103">W sekcji Ustawienia zasad hello, zaznacz **profilu edytowanie zasad** i kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Wybierz profil edytowanie zasad, a następnie kliknij przycisk Dodaj hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="ea72c-105">Wprowadź zasady **nazwa** dla tooreference Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea72c-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="ea72c-106">Na przykład wprowadź wartość `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="ea72c-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="ea72c-107">Wybierz pozycję **Dostawcy tożsamości** i zaznacz pozycję **Logowanie za pomocą konta lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="ea72c-108">Opcjonalnie możesz również wybrać dostawców tożsamości społecznościowych, jeśli są już skonfigurowani.</span><span class="sxs-lookup"><span data-stu-id="ea72c-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="ea72c-109">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-109">Click **OK**.</span></span>

![Wybierz lokalnego konta Logowanie jako dostawca tożsamości, a następnie kliknij przycisk OK hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="ea72c-111">Wybierz pozycję **Atrybuty profilu**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-111">Select **Profile attributes**.</span></span> <span data-ttu-id="ea72c-112">Wybierz atrybuty powitania klienta można wyświetlać i edytować swój profil.</span><span class="sxs-lookup"><span data-stu-id="ea72c-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="ea72c-113">Na przykład zaznacz pozycje **Kraj/Region**, **Nazwa wyświetlana** i **Kod pocztowy**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="ea72c-114">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-114">Click **OK**.</span></span>

![Wybierz niektóre atrybuty i kliknij przycisk OK hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="ea72c-116">Wybierz pozycję **Oświadczenia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-116">Select **Application claims**.</span></span> <span data-ttu-id="ea72c-117">Wybrać oświadczenia, które mają być zwracane w tokenach autoryzacji hello wysłanych wstecz tooyour aplikacji po pomyślnej sposób edytowania profilów.</span><span class="sxs-lookup"><span data-stu-id="ea72c-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="ea72c-118">Na przykład wybierz pozycje **Nazwa wyświetlana**, **Kod pocztowy**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Wybierz część oświadczeń aplikacji i kliknij przycisk OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="ea72c-120">Kliknij przycisk **Utwórz** tooadd hello zasad.</span><span class="sxs-lookup"><span data-stu-id="ea72c-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="ea72c-121">zasada Hello jest wyświetlana jako **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="ea72c-122">Witaj **B2C_1_** prefiks jest dołączany toohello nazwy.</span><span class="sxs-lookup"><span data-stu-id="ea72c-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="ea72c-123">Otwórz hello zasady, wybierając **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="ea72c-124">Sprawdź ustawienia hello określony w tabeli hello, a następnie kliknij przycisk **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="ea72c-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Wybierz zasady, a następnie uruchom je](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="ea72c-126">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="ea72c-126">Setting</span></span>      | <span data-ttu-id="ea72c-127">Wartość</span><span class="sxs-lookup"><span data-stu-id="ea72c-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="ea72c-128">**Aplikacje**</span><span class="sxs-lookup"><span data-stu-id="ea72c-128">**Applications**</span></span> | <span data-ttu-id="ea72c-129">Aplikacja Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="ea72c-129">Contoso B2C app</span></span> |
| <span data-ttu-id="ea72c-130">**Wybierz adres URL odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="ea72c-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="ea72c-131">Można sprawdzić profilu hello edytowania zgodnie z konfiguracją konsumenta i otwiera nową kartę przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="ea72c-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="ea72c-132">Zajmuje minutę tooa do tworzenia zasad on i aktualizuje tootake efekt.</span><span class="sxs-lookup"><span data-stu-id="ea72c-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>