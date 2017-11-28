---
title: "aaaAdd specyficzny dla języka firmowe tooyour strony logowania w hello Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd określonego języka firmy znakowania obrazy i tekst strony tooan Azure logowania"
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
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="16fb3-103">Dodaj specyficzne dla języka firmowe tooyour strony logowania w hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16fb3-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="16fb3-104">tooavoid pomyłek, w wielu firmach tooapply spójny wygląd i zachowanie we wszystkich hello witryn sieci Web i usługach, którymi zarządzają.</span><span class="sxs-lookup"><span data-stu-id="16fb3-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="16fb3-105">Azure Active Directory obsługuje tę funkcję, umożliwiając toocustomize wygląd hello hello strony logowania z logo firmy i niestandardowych schematów kolorów.</span><span class="sxs-lookup"><span data-stu-id="16fb3-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="16fb3-106">Strona logowania Hello jest hello strona wyświetlana podczas logowania tooOffice 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="16fb3-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="16fb3-107">Użytkownik interakcji z tej strony tooenter swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="16fb3-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="16fb3-108">Dostosowywanie hello strony logowania dla innego języka</span><span class="sxs-lookup"><span data-stu-id="16fb3-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="16fb3-109">Można dodać elementy specyficzne dla języka tooyour niestandardowe strony logowania, tylko wtedy, gdy zostały już utworzone niestandardowe strony logowania, zgodnie z opisem w [dodać znakowanie strony logowania tooyour firmowe](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16fb3-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="16fb3-110">Można skonfigurować jedną logowania stronę na katalog domyślny zestaw elementów dostosowywalnych.</span><span class="sxs-lookup"><span data-stu-id="16fb3-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="16fb3-111">Po skonfigurowaniu hello domyślny zestaw elementów strony, można skonfigurować więcej wersji dla różnych ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="16fb3-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="16fb3-112">Możesz także mieszać i dopasowywać różne elementy.</span><span class="sxs-lookup"><span data-stu-id="16fb3-112">You can also mix and match various elements.</span></span> <span data-ttu-id="16fb3-113">Na przykład można:</span><span class="sxs-lookup"><span data-stu-id="16fb3-113">For example, you could:</span></span>

* <span data-ttu-id="16fb3-114">Tworzy domyślny **logowania obraz strony** czy działającą dla wszystkich języków, następnie utworzyć specyficzne wersje dla angielskiego i francuskiego.</span><span class="sxs-lookup"><span data-stu-id="16fb3-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="16fb3-115">Po ustawieniu tooone Twojego przeglądarki z tych dwóch języków obraz specyficzny dla języka hello pojawia się, gdy ilustracja domyślna hello będzie wyświetlana dla wszystkich pozostałych języków.</span><span class="sxs-lookup"><span data-stu-id="16fb3-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="16fb3-116">Skonfigurować różne wersje logo dla organizacji (np. wersję japońską lub hebrajską).</span><span class="sxs-lookup"><span data-stu-id="16fb3-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="16fb3-117">Firma Microsoft zaleca zachowywanie hello liczby wersji języka niski, ze względu na konserwacji i wydajności.</span><span class="sxs-lookup"><span data-stu-id="16fb3-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="16fb3-118">**tooadd znakowania tooyour katalogu firmy:**</span><span class="sxs-lookup"><span data-stu-id="16fb3-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="16fb3-119">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="16fb3-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="16fb3-120">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="16fb3-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="16fb3-122">Na powitania **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.</span><span class="sxs-lookup"><span data-stu-id="16fb3-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="16fb3-123">Na powitania **użytkowników i grup - firmy znakowania** bloku, wybierz hello **Dodaj język** polecenia.</span><span class="sxs-lookup"><span data-stu-id="16fb3-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![Dodawanie znakowania elementy specyficzne dla języka](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="16fb3-125">Zmodyfikuj elementy hello ma toocustomize.</span><span class="sxs-lookup"><span data-stu-id="16fb3-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="16fb3-126">Wszystkie elementy są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="16fb3-126">All elements are optional.</span></span>
6. <span data-ttu-id="16fb3-127">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="16fb3-127">Click **Save**.</span></span>

<span data-ttu-id="16fb3-128">Może potrwać godzinę tooan dla wszystkie zmiany dokonane toohello logowania strony tooappear znakowania.</span><span class="sxs-lookup"><span data-stu-id="16fb3-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16fb3-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16fb3-129">Next steps</span></span>
[<span data-ttu-id="16fb3-130">Dodaj firmowe tooyour strony logowania</span><span class="sxs-lookup"><span data-stu-id="16fb3-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
