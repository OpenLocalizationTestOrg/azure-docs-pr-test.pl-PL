---
title: "Dostosowywanie strony logowania w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać znakowanie firmowe do platformy Azure strony logowania"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="8c954-103">Dodawanie znakowania firmowego do strony logowania w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c954-103">Add company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="8c954-104">Aby uniknąć nieporozumień, wiele firm chce zastosować spójny wygląd i zachowanie we wszystkich witrynach sieci Web i usługach, którymi zarządzają.</span><span class="sxs-lookup"><span data-stu-id="8c954-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="8c954-105">Usługa Azure Active Directory obsługuje tę funkcję, umożliwiając dostosowanie wyglądu strony logowania z logo firmy i niestandardowych schematów kolorów.</span><span class="sxs-lookup"><span data-stu-id="8c954-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="8c954-106">Strona logowania jest to strona wyświetlana podczas logowania się do usługi Office 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="8c954-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="8c954-107">Użytkownik interakcji z tej strony, aby wprowadzić swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="8c954-107">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="8c954-108">Jeśli chcesz wyświetlać swoje firmowe oznaczenia, kolory i inne dostosowywalne elementy na tej stronie, zobacz następujące ilustracje, aby zrozumieć różnicę między obydwoma środowiskami.</span><span class="sxs-lookup"><span data-stu-id="8c954-108">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="8c954-109">Poniższy zrzut ekranu przedstawia przykład strony logowania usługi Office 365 na komputerze stacjonarnym **przed** dostosowaniem:</span><span class="sxs-lookup"><span data-stu-id="8c954-109">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Strona logowania usługi Office 365 przed dostosowaniem](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="8c954-111">Poniższy zrzut ekranu przedstawia przykład strony logowania usługi Office 365 na komputerze stacjonarnym **po** dostosowaniu:</span><span class="sxs-lookup"><span data-stu-id="8c954-111">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Strona logowania usługi Office 365 po dostosowaniu](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="8c954-113">Dostosowywanie strony logowania</span><span class="sxs-lookup"><span data-stu-id="8c954-113">Customizing the sign-in page</span></span>
<span data-ttu-id="8c954-114">Zwykle na potrzeby dostępu opartego na przeglądarce do aplikacji i usług w chmurze subskrybowanych przez organizację używana jest strona logowania.</span><span class="sxs-lookup"><span data-stu-id="8c954-114">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="8c954-115">W przypadku zastosowania zmian do strony logowania uwzględnienie ich może zająć godzinę.</span><span class="sxs-lookup"><span data-stu-id="8c954-115">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="8c954-116">Strona logowania z oznaczeniami firmowymi jest wyświetlana tylko podczas odwiedzania usługi za pomocą adresu URL specyficznego dla dzierżawy, takiego jak https://outlook.com/**contoso**.com lub https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="8c954-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="8c954-117">W przypadku odwiedzania usługi za pomocą adresów URL innych niż specyficzne dla dzierżawy (np. https://mail.office365.com) wyświetlana jest strona logowania bez firmowego znakowania.</span><span class="sxs-lookup"><span data-stu-id="8c954-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="8c954-118">W takim przypadku znakowanie zostanie wyświetlone po wprowadzeniu identyfikatora użytkownika lub wybraniu kafelka użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8c954-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="8c954-119">Nazwa domeny musi występować jako "Aktywna" w **domen** części portalu Azure, w którym skonfigurowano znakowanie.</span><span class="sxs-lookup"><span data-stu-id="8c954-119">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="8c954-120">Aby uzyskać więcej informacji, zobacz [Dodawanie niestandardowych nazw domen](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8c954-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="8c954-121">Znakowanie strony logowania nie jest przenoszone na stronę logowania klienta firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8c954-121">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="8c954-122">Jeśli możesz zalogować się przy użyciu konta Microsoft, mogą zobaczyć lista kafelków użytkowników renderowana przez usługę Azure AD, ale znakowanie organizacji nie ma zastosowania do konta Microsoft Zaloguj strony.</span><span class="sxs-lookup"><span data-stu-id="8c954-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="8c954-123">Na stronie logowania pole wyboru **Nie wylogowuj mnie** umożliwia użytkownikom zachowanie stanu zalogowania w przypadku zamknięcia i ponownego otworzenia przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="8c954-123">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![Nie wylogowuj mnie](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="8c954-125">Opcja nie ma wpływu na okres istnienia sesji.</span><span class="sxs-lookup"><span data-stu-id="8c954-125">It does not effect session lifetime.</span></span> <span data-ttu-id="8c954-126">Pole wyboru na stronie logowania usługi Azure Active Directory możesz ukryć.</span><span class="sxs-lookup"><span data-stu-id="8c954-126">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="8c954-127">Określa, czy jest wyświetlane pole wyboru zależy od ustawienia **wylogowuj mnie wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="8c954-127">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![Nie wylogowuj mnie](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="8c954-129">Aby ukryć pole wyboru, należy skonfigurować to ustawienie, aby **tak**.</span><span class="sxs-lookup"><span data-stu-id="8c954-129">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="8c954-130">Niektóre funkcje usługi SharePoint Online oraz pakietu Office 2010 zależą od możliwości skorzystania z tego pola wyboru przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8c954-130">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="8c954-131">Jeśli skonfigurujesz to ustawienia na wartość „Ukryte”, użytkownicy mogą otrzymywać dodatkowe i nieoczekiwane monity o logowanie.</span><span class="sxs-lookup"><span data-stu-id="8c954-131">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="8c954-132">**Aby dodać znakowanie firmowe do katalogu:**</span><span class="sxs-lookup"><span data-stu-id="8c954-132">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="8c954-133">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="8c954-133">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="8c954-134">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="8c954-134">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="8c954-136">Na **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.</span><span class="sxs-lookup"><span data-stu-id="8c954-136">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="8c954-137">Na **użytkowników i grup - firmy znakowania** bloku, wybierz opcję **Edytuj** polecenia.</span><span class="sxs-lookup"><span data-stu-id="8c954-137">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![Edytuj niestandardowe znakowanie](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="8c954-139">Zmodyfikuj elementy, które chcesz dostosować.</span><span class="sxs-lookup"><span data-stu-id="8c954-139">Modify the elements you want to customize.</span></span> <span data-ttu-id="8c954-140">Wszystkie elementy są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="8c954-140">All elements are optional.</span></span>
6. <span data-ttu-id="8c954-141">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8c954-141">Click **Save**.</span></span>

<span data-ttu-id="8c954-142">Może potrwać do godziny wszelkie zmiany wprowadzone do strony logowania znakowania na.</span><span class="sxs-lookup"><span data-stu-id="8c954-142">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c954-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c954-143">Next steps</span></span>
[<span data-ttu-id="8c954-144">Dodać znakowanie firmowe specyficzne dla języka</span><span class="sxs-lookup"><span data-stu-id="8c954-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
