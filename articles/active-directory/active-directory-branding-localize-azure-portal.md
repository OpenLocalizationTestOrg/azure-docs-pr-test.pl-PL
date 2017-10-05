---
title: "Dodaj firmowe specyficzne dla języka do strony logowania w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać określonej firmy języka znakowania obrazy i tekst Azure stronę logowania"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="eeb59-103">Dodaj firmowe specyficzne dla języka do strony logowania w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eeb59-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="eeb59-104">Aby uniknąć nieporozumień, wiele firm chce zastosować spójny wygląd i zachowanie we wszystkich witrynach sieci Web i usługach, którymi zarządzają.</span><span class="sxs-lookup"><span data-stu-id="eeb59-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="eeb59-105">Usługa Azure Active Directory obsługuje tę funkcję, umożliwiając dostosowanie wyglądu strony logowania z logo firmy i niestandardowych schematów kolorów.</span><span class="sxs-lookup"><span data-stu-id="eeb59-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="eeb59-106">Strona logowania jest to strona wyświetlana podczas logowania się do usługi Office 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="eeb59-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="eeb59-107">Użytkownik interakcji z tej strony, aby wprowadzić swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="eeb59-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="eeb59-108">Dostosowywanie strony logowania dla innego języka</span><span class="sxs-lookup"><span data-stu-id="eeb59-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="eeb59-109">Możesz dodać elementy specyficzne dla języka do niestandardowej strony logowania tylko wtedy, gdy zostały już utworzone niestandardowe strony logowania, zgodnie z opisem w [dodać znakowanie firmowe do strony logowania](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eeb59-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="eeb59-110">Można skonfigurować jedną logowania stronę na katalog domyślny zestaw elementów dostosowywalnych.</span><span class="sxs-lookup"><span data-stu-id="eeb59-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="eeb59-111">Po skonfigurowaniu domyślny zestaw elementów strony, można skonfigurować więcej wersji dla różnych ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="eeb59-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="eeb59-112">Możesz także mieszać i dopasowywać różne elementy.</span><span class="sxs-lookup"><span data-stu-id="eeb59-112">You can also mix and match various elements.</span></span> <span data-ttu-id="eeb59-113">Na przykład można:</span><span class="sxs-lookup"><span data-stu-id="eeb59-113">For example, you could:</span></span>

* <span data-ttu-id="eeb59-114">Tworzy domyślny **logowania obraz strony** czy działającą dla wszystkich języków, następnie utworzyć specyficzne wersje dla angielskiego i francuskiego.</span><span class="sxs-lookup"><span data-stu-id="eeb59-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="eeb59-115">Po ustawieniu przeglądarek do jednej z tych dwóch języków pojawia się obraz specyficzny dla języka, podczas gdy ilustracja domyślna będzie wyświetlana dla wszystkich pozostałych języków.</span><span class="sxs-lookup"><span data-stu-id="eeb59-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="eeb59-116">Skonfigurować różne wersje logo dla organizacji (np. wersję japońską lub hebrajską).</span><span class="sxs-lookup"><span data-stu-id="eeb59-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="eeb59-117">Firma Microsoft zaleca zachowywanie liczby wersji języka niski, ze względu na konserwacji i wydajności.</span><span class="sxs-lookup"><span data-stu-id="eeb59-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="eeb59-118">**Aby dodać znakowanie firmowe do katalogu:**</span><span class="sxs-lookup"><span data-stu-id="eeb59-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="eeb59-119">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="eeb59-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="eeb59-120">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="eeb59-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="eeb59-122">Na **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.</span><span class="sxs-lookup"><span data-stu-id="eeb59-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="eeb59-123">Na **użytkowników i grup - firmy znakowania** bloku, wybierz opcję **Dodaj język** polecenia.</span><span class="sxs-lookup"><span data-stu-id="eeb59-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![Dodawanie znakowania elementy specyficzne dla języka](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="eeb59-125">Zmodyfikuj elementy, które chcesz dostosować.</span><span class="sxs-lookup"><span data-stu-id="eeb59-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="eeb59-126">Wszystkie elementy są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="eeb59-126">All elements are optional.</span></span>
6. <span data-ttu-id="eeb59-127">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="eeb59-127">Click **Save**.</span></span>

<span data-ttu-id="eeb59-128">Może potrwać do godziny wszelkie zmiany wprowadzone do strony logowania znakowania na.</span><span class="sxs-lookup"><span data-stu-id="eeb59-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eeb59-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eeb59-129">Next steps</span></span>
[<span data-ttu-id="eeb59-130">Dodawanie znakowania firmowego do strony logowania</span><span class="sxs-lookup"><span data-stu-id="eeb59-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
