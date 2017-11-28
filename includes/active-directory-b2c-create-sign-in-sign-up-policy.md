<span data-ttu-id="baabf-101">Aby włączyć logowanie w swojej aplikacji, musisz utworzyć zasady logowania.</span><span class="sxs-lookup"><span data-stu-id="baabf-101">To enable sign-in on your application, you will need to create a sign-in policy.</span></span> <span data-ttu-id="baabf-102">Te zasady opisują procesy, przez które przejdą użytkownicy podczas logowania, i zawartość tokenów, które aplikacja otrzyma po pomyślnych logowaniach.</span><span class="sxs-lookup"><span data-stu-id="baabf-102">This policy describes the experiences that consumers will go through during sign-in and the contents of tokens that the application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="baabf-103">W sekcji ustawień dotyczącej zasad wybierz pozycję **Zasady logowania lub tworzenia konta** i kliknij pozycję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="baabf-103">In the policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Wybierz zasady rejestracji lub logowania i kliknij przycisk Dodaj](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="baabf-105">Wprowadź **Nazwę** zasad, do której będzie odwoływać się Twoja aplikacja.</span><span class="sxs-lookup"><span data-stu-id="baabf-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="baabf-106">Na przykład wprowadź wartość `SiUpIn`.</span><span class="sxs-lookup"><span data-stu-id="baabf-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="baabf-107">Wybierz pozycję **Dostawcy tożsamości** i zaznacz pozycję **Tworzenie konta za pomocą adresu e-mail**.</span><span class="sxs-lookup"><span data-stu-id="baabf-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="baabf-108">Opcjonalnie możesz również wybrać dostawców tożsamości społecznościowych, jeśli są już skonfigurowani.</span><span class="sxs-lookup"><span data-stu-id="baabf-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="baabf-109">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="baabf-109">Click **OK**.</span></span>

![Wybierz rejestrację za pomocą adresu e-mail, a następnie kliknij przycisk OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="baabf-111">Wybierz pozycję **Atrybuty tworzenia konta**.</span><span class="sxs-lookup"><span data-stu-id="baabf-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="baabf-112">Wybierz atrybuty, które mają być zbierane od użytkownika podczas rejestracji.</span><span class="sxs-lookup"><span data-stu-id="baabf-112">Choose attributes you want to collect from the consumer during sign-up.</span></span> <span data-ttu-id="baabf-113">Na przykład zaznacz pozycje **Kraj/Region**, **Nazwa wyświetlana** i **Kod pocztowy**.</span><span class="sxs-lookup"><span data-stu-id="baabf-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="baabf-114">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="baabf-114">Click **OK**.</span></span>

![Wybierz część atrybutów, a następnie kliknij przycisk OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="baabf-116">Wybierz pozycję **Oświadczenia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="baabf-116">Select **Application claims**.</span></span> <span data-ttu-id="baabf-117">Wybierz oświadczenia, które mają być zwracane w tokenach autoryzacji wysyłanych z powrotem do Twojej aplikacji po pomyślnej rejestracji lub zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="baabf-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="baabf-118">Na przykład wybierz pozycje **Nazwa wyświetlana**, **Dostawca tożsamości**, **Kod pocztowy**, **Użytkownik jest nowy** i **Identyfikator obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="baabf-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Wybierz część oświadczeń aplikacji i kliknij przycisk OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="baabf-120">Kliknij przycisk **Utwórz**, aby dodać zasady.</span><span class="sxs-lookup"><span data-stu-id="baabf-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="baabf-121">Zasada jest wyświetlana jako **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="baabf-121">The policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="baabf-122">Do nazwy jest dołączany prefiks **B2C_1_**.</span><span class="sxs-lookup"><span data-stu-id="baabf-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="baabf-123">Otwórz zasady, wybierając pozycję **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="baabf-123">Open the policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="baabf-124">Sprawdź ustawienia określone w tabeli, a następnie kliknij pozycję **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="baabf-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Wybierz zasady, a następnie uruchom je](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="baabf-126">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="baabf-126">Setting</span></span>      | <span data-ttu-id="baabf-127">Wartość</span><span class="sxs-lookup"><span data-stu-id="baabf-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="baabf-128">**Aplikacje**</span><span class="sxs-lookup"><span data-stu-id="baabf-128">**Applications**</span></span> | <span data-ttu-id="baabf-129">Aplikacja Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="baabf-129">Contoso B2C app</span></span> |
| <span data-ttu-id="baabf-130">**Wybierz adres URL odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="baabf-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="baabf-131">Zostanie otwarta nowa karta przeglądarki, na której możesz sprawdzić, czy rejestrowanie lub logowanie użytkownika przebiega tak, jak zostało skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="baabf-131">A new browser tab opens, and you can verify the sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="baabf-132">Utworzenie zasad i zastosowanie aktualizacji zajmuje do minuty.</span><span class="sxs-lookup"><span data-stu-id="baabf-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>