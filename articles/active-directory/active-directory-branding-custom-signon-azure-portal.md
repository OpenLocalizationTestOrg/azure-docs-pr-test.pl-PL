---
title: Logowanie w obszarze hello Azure Active Directory aaaCustomize | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooadd strony toohello Azure logowania w znakowaniu firmy"
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
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="bb201-103">Dodaj firmowe tooyour strony logowania w hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb201-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="bb201-104">tooavoid pomyłek, w wielu firmach tooapply spójny wygląd i zachowanie we wszystkich hello witryn sieci Web i usługach, którymi zarządzają.</span><span class="sxs-lookup"><span data-stu-id="bb201-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="bb201-105">Azure Active Directory obsługuje tę funkcję, umożliwiając toocustomize wygląd hello hello strony logowania z logo firmy i niestandardowych schematów kolorów.</span><span class="sxs-lookup"><span data-stu-id="bb201-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="bb201-106">Strona logowania Hello jest hello strona wyświetlana podczas logowania tooOffice 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="bb201-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="bb201-107">Użytkownik interakcji z tej strony tooenter swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="bb201-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="bb201-108">Jeśli chcesz tooshow swoje firmowe oznaczenia, kolory i inne dostosowywalne elementy na tej stronie, zobacz następujące obrazy toounderstand hello różnicę między obydwoma środowiskami hello hello.</span><span class="sxs-lookup"><span data-stu-id="bb201-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="bb201-109">Witaj, wykonując zrzut ekranu przedstawia oraz przykład dla usługi Office 365 hello strony logowania na komputerze stacjonarnym **przed** dostosowaniem:</span><span class="sxs-lookup"><span data-stu-id="bb201-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Strona logowania usługi Office 365 przed dostosowaniem](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="bb201-111">Witaj, wykonując zrzut ekranu przedstawia oraz przykład dla usługi Office 365 hello strony logowania na komputerze stacjonarnym **po** dostosowaniem:</span><span class="sxs-lookup"><span data-stu-id="bb201-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Strona logowania usługi Office 365 po dostosowaniu](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="bb201-113">Dostosowywanie strony logowania hello</span><span class="sxs-lookup"><span data-stu-id="bb201-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="bb201-114">Zwykle dostęp za pośrednictwem przeglądarki tooyour chmury aplikacji i usług, które subskrybuje Twoja organizacja, należy użyć hello strony logowania.</span><span class="sxs-lookup"><span data-stu-id="bb201-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="bb201-115">Jeśli strona logowania tooyour zmiany zostały zastosowane, może potrwać do godziny tooan hello tooappear zmiany.</span><span class="sxs-lookup"><span data-stu-id="bb201-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="bb201-116">Strona logowania z oznaczeniami firmowymi jest wyświetlana tylko podczas odwiedzania usługi za pomocą adresu URL specyficznego dla dzierżawy, takiego jak https://outlook.com/**contoso**.com lub https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="bb201-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="bb201-117">W przypadku odwiedzania usługi za pomocą adresów URL innych niż specyficzne dla dzierżawy (np. https://mail.office365.com) wyświetlana jest strona logowania bez firmowego znakowania.</span><span class="sxs-lookup"><span data-stu-id="bb201-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="bb201-118">W takim przypadku znakowanie zostanie wyświetlone po wprowadzeniu identyfikatora użytkownika lub wybraniu kafelka użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bb201-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="bb201-119">Nazwa domeny musi występować jako "Aktywna" w hello **domen** część hello portalu Azure, w którym skonfigurowano znakowanie.</span><span class="sxs-lookup"><span data-stu-id="bb201-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="bb201-120">Aby uzyskać więcej informacji, zobacz [Dodawanie niestandardowych nazw domen](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bb201-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="bb201-121">Znakowanie strony logowania nie jest przenoszone toohello konsumenta logowania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bb201-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="bb201-122">Jeśli możesz zalogować się przy użyciu konta Microsoft, mogą zobaczyć lista kafelków użytkowników renderowana przez usługę Azure AD, ale hello znakowanie organizacji nie ma zastosowania toohello strony logowania na koncie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bb201-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="bb201-123">Na stronie logowania hello **wylogowuj mnie** wyboru pozwala tooremain użytkownik zalogowany po ich zamknięcie i ponowne otwarcie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="bb201-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![Nie wylogowuj mnie](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="bb201-125">Opcja nie ma wpływu na okres istnienia sesji.</span><span class="sxs-lookup"><span data-stu-id="bb201-125">It does not effect session lifetime.</span></span> <span data-ttu-id="bb201-126">Pole wyboru hello na stronę logowania w usłudze Azure Active Directory hello można ukryć.</span><span class="sxs-lookup"><span data-stu-id="bb201-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="bb201-127">Określa, czy pole wyboru hello jest wyświetlane zależy od ustawienia hello **wylogowuj mnie wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="bb201-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![Nie wylogowuj mnie](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="bb201-129">toohide wyboru hello, skonfiguruj to ustawienie zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="bb201-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="bb201-130">Niektóre funkcje pakietu Office 2010 i SharePoint Online są zależne od użytkownicy będą mogli toocheck tego pola.</span><span class="sxs-lookup"><span data-stu-id="bb201-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="bb201-131">Jeśli konfigurujesz toohidden to ustawienie, dodatkowe i nieoczekiwane monity toosign w może widzą użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bb201-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="bb201-132">**tooadd znakowania tooyour katalogu firmy:**</span><span class="sxs-lookup"><span data-stu-id="bb201-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="bb201-133">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="bb201-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="bb201-134">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bb201-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="bb201-136">Na powitania **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.</span><span class="sxs-lookup"><span data-stu-id="bb201-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="bb201-137">Na powitania **użytkowników i grup - firmy znakowania** bloku, wybierz hello **Edytuj** polecenia.</span><span class="sxs-lookup"><span data-stu-id="bb201-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![Edytuj niestandardowe znakowanie](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="bb201-139">Zmodyfikuj elementy hello ma toocustomize.</span><span class="sxs-lookup"><span data-stu-id="bb201-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="bb201-140">Wszystkie elementy są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="bb201-140">All elements are optional.</span></span>
6. <span data-ttu-id="bb201-141">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="bb201-141">Click **Save**.</span></span>

<span data-ttu-id="bb201-142">Może potrwać godzinę tooan dla wszystkie zmiany dokonane toohello logowania strony tooappear znakowania.</span><span class="sxs-lookup"><span data-stu-id="bb201-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb201-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bb201-143">Next steps</span></span>
[<span data-ttu-id="bb201-144">Dodać znakowanie firmowe specyficzne dla języka</span><span class="sxs-lookup"><span data-stu-id="bb201-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
