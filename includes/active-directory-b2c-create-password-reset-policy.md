<span data-ttu-id="0c798-101">hasło szczegółowych tooenable zresetować w swojej aplikacji, konieczne będzie toocreate zasady resetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="0c798-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="0c798-102">Uwaga określono opcję resetowania hasła na poziomie dzierżawy tego hello [tutaj](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="0c798-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="0c798-103">Ta zasada opisuje hello procesów, które konsumentów hello będzie przejście przez podczas resetowania hasła i zawartość hello tokeny hello aplikacji zostanie wyświetlony po pomyślnym ukończeniu.</span><span class="sxs-lookup"><span data-stu-id="0c798-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="0c798-104">W sekcji Ustawienia zasad hello, zaznacz **zasady resetowania hasła** i kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0c798-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Wybierz zasady rejestracji i logowania i kliknij przycisk Dodaj hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="0c798-106">Wprowadź zasady **nazwa** dla tooreference Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0c798-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="0c798-107">Na przykład wprowadź wartość `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="0c798-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="0c798-108">Wybierz pozycję **Dostawcy tożsamości** i zaznacz pozycję **Resetuj hasło przy użyciu adresu e-mail**.</span><span class="sxs-lookup"><span data-stu-id="0c798-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="0c798-109">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c798-109">Click **OK**.</span></span>

![Wybierz resetowania hasła przy użyciu adresu e-mail jako dostawca tożsamości, a następnie kliknij przycisk OK hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="0c798-111">Wybierz pozycję **Oświadczenia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="0c798-111">Select **Application claims**.</span></span> <span data-ttu-id="0c798-112">Wybrać oświadczenia, które mają być zwracane w tokenach autoryzacji hello wysyłane aplikacji tooyour wstecz po funkcji resetowania hasła powiodło się.</span><span class="sxs-lookup"><span data-stu-id="0c798-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="0c798-113">Na przykład wybierz pozycję **Identyfikator obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="0c798-113">For example, select **User's Object ID**.</span></span>

![Wybierz część oświadczeń aplikacji i kliknij przycisk OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="0c798-115">Kliknij przycisk **Utwórz** tooadd hello zasad.</span><span class="sxs-lookup"><span data-stu-id="0c798-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="0c798-116">zasada Hello jest wyświetlana jako **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="0c798-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="0c798-117">Witaj **B2C_1_** prefiks jest dołączany toohello nazwy.</span><span class="sxs-lookup"><span data-stu-id="0c798-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="0c798-118">Otwórz hello zasady, wybierając **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="0c798-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="0c798-119">Sprawdź ustawienia hello określony w tabeli hello, a następnie kliknij przycisk **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="0c798-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Wybierz zasady, a następnie uruchom je](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="0c798-121">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="0c798-121">Setting</span></span>      | <span data-ttu-id="0c798-122">Wartość</span><span class="sxs-lookup"><span data-stu-id="0c798-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="0c798-123">**Aplikacje**</span><span class="sxs-lookup"><span data-stu-id="0c798-123">**Applications**</span></span> | <span data-ttu-id="0c798-124">Aplikacja Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="0c798-124">Contoso B2C app</span></span> |
| <span data-ttu-id="0c798-125">**Wybierz adres URL odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="0c798-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="0c798-126">Otwiera nową kartę przeglądarki i możesz sprawdzić, czy resetowania hasła hello korzystanie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0c798-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-127">Zajmuje minutę tooa do tworzenia zasad on i aktualizuje tootake efekt.</span><span class="sxs-lookup"><span data-stu-id="0c798-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
