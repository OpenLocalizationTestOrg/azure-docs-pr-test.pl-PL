<span data-ttu-id="d90b1-101">Aby włączyć precyzyjne resetowanie haseł w swojej aplikacji, musisz utworzyć zasady resetowania haseł.</span><span class="sxs-lookup"><span data-stu-id="d90b1-101">To enable fine-grained password reset on your application, you will need to create a password reset policy.</span></span> <span data-ttu-id="d90b1-102">Pamiętaj, że opcja resetowania haseł na poziomie całej dzierżawy została określona [tutaj](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="d90b1-102">Note that the tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="d90b1-103">Te zasady opisują procesy, przez które przejdą użytkownicy podczas resetowania haseł, i zawartość tokenów, które aplikacja otrzyma po ich pomyślnym ukończeniu.</span><span class="sxs-lookup"><span data-stu-id="d90b1-103">This policy describes the experiences that the consumers will go through during password reset and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="d90b1-104">W sekcji ustawień dotyczącej zasad wybierz pozycję **Zasady resetowania hasła** i kliknij pozycję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d90b1-104">In the policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Wybierz zasady rejestracji lub logowania i kliknij przycisk Dodaj](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="d90b1-106">Wprowadź **Nazwę** zasad, do której będzie odwoływać się Twoja aplikacja.</span><span class="sxs-lookup"><span data-stu-id="d90b1-106">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="d90b1-107">Na przykład wprowadź wartość `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="d90b1-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="d90b1-108">Wybierz pozycję **Dostawcy tożsamości** i zaznacz pozycję **Resetuj hasło przy użyciu adresu e-mail**.</span><span class="sxs-lookup"><span data-stu-id="d90b1-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="d90b1-109">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d90b1-109">Click **OK**.</span></span>

![Wybierz resetowanie hasła przy użyciu adresu e-mail jako dostawcy tożsamości, a następnie kliknij przycisk OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="d90b1-111">Wybierz pozycję **Oświadczenia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="d90b1-111">Select **Application claims**.</span></span> <span data-ttu-id="d90b1-112">Wybierz oświadczenia, które mają być zwracane w tokenach autoryzacji odsyłanych do Twojej aplikacji po pomyślnym zresetowaniu hasła.</span><span class="sxs-lookup"><span data-stu-id="d90b1-112">Choose claims you want returned in the authorization tokens sent back to your application after a successful password reset experience.</span></span> <span data-ttu-id="d90b1-113">Na przykład wybierz pozycję **Identyfikator obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d90b1-113">For example, select **User's Object ID**.</span></span>

![Wybierz część oświadczeń aplikacji i kliknij przycisk OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="d90b1-115">Kliknij przycisk **Utwórz**, aby dodać zasady.</span><span class="sxs-lookup"><span data-stu-id="d90b1-115">Click **Create** to add the policy.</span></span> <span data-ttu-id="d90b1-116">Zasady są wyświetlane jako **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="d90b1-116">The policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="d90b1-117">Do nazwy jest dołączany prefiks **B2C_1_**.</span><span class="sxs-lookup"><span data-stu-id="d90b1-117">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="d90b1-118">Otwórz zasady, wybierając pozycję **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="d90b1-118">Open the policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="d90b1-119">Sprawdź ustawienia określone w tabeli, a następnie kliknij pozycję **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="d90b1-119">Verify the settings specified in the table then click **Run now**.</span></span>

![Wybierz zasady, a następnie uruchom je](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="d90b1-121">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="d90b1-121">Setting</span></span>      | <span data-ttu-id="d90b1-122">Wartość</span><span class="sxs-lookup"><span data-stu-id="d90b1-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="d90b1-123">**Aplikacje**</span><span class="sxs-lookup"><span data-stu-id="d90b1-123">**Applications**</span></span> | <span data-ttu-id="d90b1-124">Aplikacja Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="d90b1-124">Contoso B2C app</span></span> |
| <span data-ttu-id="d90b1-125">**Wybierz adres URL odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="d90b1-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="d90b1-126">Zostanie otwarta nowa karta przeglądarki i możesz sprawdzić działanie resetowania hasła użytkownika w Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d90b1-126">A new browser tab opens, and you can verify the password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="d90b1-127">Utworzenie zasad i zastosowanie aktualizacji zajmuje do minuty.</span><span class="sxs-lookup"><span data-stu-id="d90b1-127">It takes up to a minute for policy creation and updates to take effect.</span></span>
>
