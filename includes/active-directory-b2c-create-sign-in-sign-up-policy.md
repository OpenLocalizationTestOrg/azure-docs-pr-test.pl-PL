<span data-ttu-id="eecad-101">Logowanie tooenable dla aplikacji, konieczne będzie zasad toocreate logowania.</span><span class="sxs-lookup"><span data-stu-id="eecad-101">tooenable sign-in on your application, you will need toocreate a sign-in policy.</span></span> <span data-ttu-id="eecad-102">Ta zasada opis hello procesów, które konsumentów będzie przejście przez podczas logowania i zawartość hello tokeny hello aplikacji zostanie wyświetlony na pomyślne logowania.</span><span class="sxs-lookup"><span data-stu-id="eecad-102">This policy describes hello experiences that consumers will go through during sign-in and hello contents of tokens that hello application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="eecad-103">W sekcji Ustawienia zasad hello, zaznacz **zasad rejestracji i logowania** i kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eecad-103">In hello policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Wybierz zasady rejestracji lub logowania i kliknij przycisk Dodaj](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="eecad-105">Wprowadź zasady **nazwa** dla tooreference Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eecad-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="eecad-106">Na przykład wprowadź wartość `SiUpIn`.</span><span class="sxs-lookup"><span data-stu-id="eecad-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="eecad-107">Wybierz pozycję **Dostawcy tożsamości** i zaznacz pozycję **Tworzenie konta za pomocą adresu e-mail**.</span><span class="sxs-lookup"><span data-stu-id="eecad-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="eecad-108">Opcjonalnie możesz również wybrać dostawców tożsamości społecznościowych, jeśli są już skonfigurowani.</span><span class="sxs-lookup"><span data-stu-id="eecad-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="eecad-109">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="eecad-109">Click **OK**.</span></span>

![Wybierz zapisywania wiadomości E-mail jako dostawca tożsamości i kliknij przycisk OK hello](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="eecad-111">Wybierz pozycję **Atrybuty tworzenia konta**.</span><span class="sxs-lookup"><span data-stu-id="eecad-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="eecad-112">Wybierz atrybuty ma toocollect od konsumenta hello podczas tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="eecad-112">Choose attributes you want toocollect from hello consumer during sign-up.</span></span> <span data-ttu-id="eecad-113">Na przykład zaznacz pozycje **Kraj/Region**, **Nazwa wyświetlana** i **Kod pocztowy**.</span><span class="sxs-lookup"><span data-stu-id="eecad-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="eecad-114">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="eecad-114">Click **OK**.</span></span>

![Wybierz niektóre atrybuty i kliknij przycisk OK hello](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="eecad-116">Wybierz pozycję **Oświadczenia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="eecad-116">Select **Application claims**.</span></span> <span data-ttu-id="eecad-117">Wybrać oświadczenia, które mają być zwracane w tokenach autoryzacji hello wysłanych wstecz tooyour aplikacji po pomyślnej rejestracji lub logowania systemu.</span><span class="sxs-lookup"><span data-stu-id="eecad-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="eecad-118">Na przykład wybierz pozycje **Nazwa wyświetlana**, **Dostawca tożsamości**, **Kod pocztowy**, **Użytkownik jest nowy** i **Identyfikator obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="eecad-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Wybierz część oświadczeń aplikacji i kliknij przycisk OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="eecad-120">Kliknij przycisk **Utwórz** tooadd hello zasad.</span><span class="sxs-lookup"><span data-stu-id="eecad-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="eecad-121">zasada Hello jest wyświetlana jako **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="eecad-121">hello policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="eecad-122">Witaj **B2C_1_** prefiks jest dołączany toohello nazwy.</span><span class="sxs-lookup"><span data-stu-id="eecad-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="eecad-123">Otwórz hello zasady, wybierając **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="eecad-123">Open hello policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="eecad-124">Sprawdź ustawienia hello określony w tabeli hello, a następnie kliknij przycisk **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="eecad-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Wybierz zasady, a następnie uruchom je](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="eecad-126">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="eecad-126">Setting</span></span>      | <span data-ttu-id="eecad-127">Wartość</span><span class="sxs-lookup"><span data-stu-id="eecad-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="eecad-128">**Aplikacje**</span><span class="sxs-lookup"><span data-stu-id="eecad-128">**Applications**</span></span> | <span data-ttu-id="eecad-129">Aplikacja Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="eecad-129">Contoso B2C app</span></span> |
| <span data-ttu-id="eecad-130">**Wybierz adres URL odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="eecad-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="eecad-131">Można sprawdzić hello środowisko rejestracji i logowania użytkownika, zgodnie z konfiguracją i otwiera nową kartę przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="eecad-131">A new browser tab opens, and you can verify hello sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="eecad-132">Zajmuje minutę tooa do tworzenia zasad on i aktualizuje tootake efekt.</span><span class="sxs-lookup"><span data-stu-id="eecad-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>