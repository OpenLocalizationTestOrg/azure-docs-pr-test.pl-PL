<span data-ttu-id="bfe26-101">Aby włączyć edytowanie profilu w Twojej aplikacji, musisz utworzyć zasady edytowania profilu.</span><span class="sxs-lookup"><span data-stu-id="bfe26-101">To enable profile editing on your application, you will need to create a profile editing policy.</span></span> <span data-ttu-id="bfe26-102">Te zasady opisują procesy, przez które przejdą użytkownicy podczas edytowania profilu, i zawartość tokenów, które aplikacja otrzyma po pomyślnym ich ukończeniu.</span><span class="sxs-lookup"><span data-stu-id="bfe26-102">This policy describes the experiences that consumers will go through during profile editing and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="bfe26-103">W sekcji ustawień dotyczących zasad wybierz pozycję **Zasady edytowania profilu** i kliknij pozycję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-103">In the policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Wybierz pozycję Zasady edytowania profilu, a następnie kliknij przycisk Dodaj](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="bfe26-105">Wprowadź **Nazwę** zasad, do której będzie odwoływać się Twoja aplikacja.</span><span class="sxs-lookup"><span data-stu-id="bfe26-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="bfe26-106">Na przykład wprowadź wartość `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="bfe26-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="bfe26-107">Wybierz pozycję **Dostawcy tożsamości** i zaznacz pozycję **Logowanie za pomocą konta lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="bfe26-108">Opcjonalnie możesz również wybrać dostawców tożsamości społecznościowych, jeśli są już skonfigurowani.</span><span class="sxs-lookup"><span data-stu-id="bfe26-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="bfe26-109">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-109">Click **OK**.</span></span>

![Wybierz pozycję Logowanie za pomocą konta lokalnego jako dostawcę tożsamości, a następnie kliknij przycisk OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="bfe26-111">Wybierz pozycję **Atrybuty profilu**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-111">Select **Profile attributes**.</span></span> <span data-ttu-id="bfe26-112">Wybierz atrybuty, które użytkownik może wyświetlać i edytować w swoim profilu.</span><span class="sxs-lookup"><span data-stu-id="bfe26-112">Choose attributes the consumer can view and edit in their profile.</span></span> <span data-ttu-id="bfe26-113">Na przykład zaznacz pozycje **Kraj/Region**, **Nazwa wyświetlana** i **Kod pocztowy**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="bfe26-114">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-114">Click **OK**.</span></span>

![Wybierz część atrybutów, a następnie kliknij przycisk OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="bfe26-116">Wybierz pozycję **Oświadczenia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-116">Select **Application claims**.</span></span> <span data-ttu-id="bfe26-117">Wybierz oświadczenia, które mają być zwracane w tokenach autoryzacji wysyłanych z powrotem do aplikacji po pomyślnym edytowaniu profilu.</span><span class="sxs-lookup"><span data-stu-id="bfe26-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful profile editing experience.</span></span> <span data-ttu-id="bfe26-118">Na przykład wybierz pozycje **Nazwa wyświetlana**, **Kod pocztowy**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Wybierz część oświadczeń aplikacji i kliknij przycisk OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="bfe26-120">Kliknij przycisk **Utwórz**, aby dodać zasady.</span><span class="sxs-lookup"><span data-stu-id="bfe26-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="bfe26-121">Zasady są wyświetlane jako **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-121">The policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="bfe26-122">Do nazwy jest dołączany prefiks **B2C_1_**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="bfe26-123">Otwórz zasady, wybierając pozycję **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-123">Open the policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="bfe26-124">Sprawdź ustawienia określone w tabeli, a następnie kliknij pozycję **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="bfe26-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Wybierz zasady, a następnie uruchom je](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="bfe26-126">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="bfe26-126">Setting</span></span>      | <span data-ttu-id="bfe26-127">Wartość</span><span class="sxs-lookup"><span data-stu-id="bfe26-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="bfe26-128">**Aplikacje**</span><span class="sxs-lookup"><span data-stu-id="bfe26-128">**Applications**</span></span> | <span data-ttu-id="bfe26-129">Aplikacja Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="bfe26-129">Contoso B2C app</span></span> |
| <span data-ttu-id="bfe26-130">**Wybierz adres URL odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="bfe26-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="bfe26-131">Zostanie otwarta nowa karta przeglądarki, na której możesz sprawdzić, czy edytowanie profilu użytkownika działa tak, jak zostało skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="bfe26-131">A new browser tab opens, and you can verify the profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="bfe26-132">Utworzenie zasad i zastosowanie aktualizacji zajmuje do minuty.</span><span class="sxs-lookup"><span data-stu-id="bfe26-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>