---
title: Wprowadzenie do aplikacji Azure AD Privileged Identity Management | Microsoft Docs
description: "Informacje o sposobie zarządzania uprzywilejowanymi tożsamościami przy użyciu aplikacji Azure Active Directory Privileged Identity Management w witrynie Azure Portal."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 17cdff033cc3dbb199d11c3b8ac1acbc92499877
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a><span data-ttu-id="ff7e9-103">Rozpoczynanie używania aplikacji Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="ff7e9-103">Start using Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="ff7e9-104">Aplikacja Azure Active Directory (AD) Privileged Identity Management umożliwia kontrolę i monitorowanie dostępu, a także zarządzanie nim w ramach danej organizacji.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="ff7e9-105">Ten zakres obejmuje dostęp do zasobów usługi Azure AD i innych usług online firmy Microsoft, takich jak Office 365 lub Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-105">This scope includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="ff7e9-106">W tym artykule wyjaśniono, jak dodać aplikację Azure AD PIM do pulpitu nawigacyjnego witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="ff7e9-107">Dodawanie aplikacji Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="ff7e9-107">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="ff7e9-108">Przed użyciem aplikacji Azure AD Privileged Identity Management należy dodać ją do pulpitu nawigacyjnego witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-108">Before you use Azure AD Privileged Identity Management, you need to add the application to your Azure portal dashboard.</span></span>

1. <span data-ttu-id="ff7e9-109">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/) jako administrator globalny katalogu.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-109">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="ff7e9-110">Jeśli organizacja dysponuje więcej niż jednym katalogiem, wybierz swoją nazwę użytkownika w prawym górnym rogu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-110">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="ff7e9-111">Wybierz katalog, w którym chcesz używać aplikacji PIM.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-111">Select the directory where you want to use PIM.</span></span>
3. <span data-ttu-id="ff7e9-112">Wybierz polecenie **Więcej usług** i użyj pola tekstowego filtru, aby wyszukać **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-112">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="ff7e9-113">Zaznacz opcję **Przypnij do pulpitu nawigacyjnego**, a następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-113">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="ff7e9-114">Nastąpi otwarcie aplikacji Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-114">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="ff7e9-115">Jeśli jesteś pierwszą osobą używającą usługi Azure AD Privileged Identity Management w katalogu, będziesz mieć automatycznie przypisane role **Administrator zabezpieczeń** i **Administrator ról uprzywilejowanych** w katalogu.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-115">If you're the first person to use Azure AD Privileged Identity Management in your directory, you are automatically assigned the **Security administrator** and **Privileged role administrator** roles in the directory.</span></span> <span data-ttu-id="ff7e9-116">Tylko administratorzy ról uprzywilejowanych mogą zarządzać przypisaniami ról użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-116">Only privileged role administrators can manage role assignments of users.</span></span> <span data-ttu-id="ff7e9-117">Ponadto można zdecydować się na uruchomienie [kreatora zabezpieczeń](active-directory-privileged-identity-management-security-wizard.md),</span><span class="sxs-lookup"><span data-stu-id="ff7e9-117">In addition, you may choose to run the [security wizard.](active-directory-privileged-identity-management-security-wizard.md)</span></span> <span data-ttu-id="ff7e9-118">który przeprowadzi Cię przez środowisko początkowego odnajdywania i przypisywania.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-118">that walks you through the initial discovery and assignment experience.</span></span>

## <a name="navigate-to-your-tasks"></a><span data-ttu-id="ff7e9-119">Przejdź do zadań</span><span class="sxs-lookup"><span data-stu-id="ff7e9-119">Navigate to your tasks</span></span>
<span data-ttu-id="ff7e9-120">Po skonfigurowaniu usługi Azure AD Privileged Identity Management zobaczysz blok nawigacji pojawiający się przy każdym otwarciu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-120">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span> <span data-ttu-id="ff7e9-121">Użyj tego bloku w celu wykonywania zadań związanych z zarządzaniem tożsamościami.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-121">Use this blade to accomplish your identity management tasks.</span></span>

![Zrzut ekranu przedstawiający zadania najwyższego poziomu dla aplikacji PIM](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* <span data-ttu-id="ff7e9-123">Opcja **Moje role** przenosi Cię do listy ról przypisanych do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-123">**My Roles** takes you to a list of roles that are assigned to you.</span></span> <span data-ttu-id="ff7e9-124">W tej sekcji będzie można aktywować wszystkie role, które danemu użytkownikowi przysługują.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-124">This section is where you activate any roles that you are eligible for.</span></span>
* <span data-ttu-id="ff7e9-125">Opcja **Zatwierdzanie żądań (wersja zapoznawcza)** powoduje wyświetlenie listy oczekujących żądań aktywacji od użytkowników w katalogu.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-125">**Approve Requests (Preview)** displays a list of pending activation requests from users in your directory.</span></span> [<span data-ttu-id="ff7e9-126">Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-126">Learn more.</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* <span data-ttu-id="ff7e9-127">Opcja **Oczekujące żądania (wersja zapoznawcza)** powoduje wyświetlenie bieżących żądań oczekujących na aktywację.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-127">**Pending Requests (Preview)** displays any current requests to have made to activate.</span></span>
* <span data-ttu-id="ff7e9-128">Opcja **Sprawdź dostęp** przenosi Cię do oczekujących przeglądów dostępu, które należy wykonać niezależnie od tego, czy przeglądasz dostęp dla siebie lub kogoś innego.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-128">**Review Access** takes you to any pending access reviews that you need to complete, whether you're reviewing access for yourself or someone else.</span></span>
* <span data-ttu-id="ff7e9-129">Opcja **Role w katalogach usługi Azure AD** dostępna w obszarze zarządzania jest pulpitem nawigacyjnym dla administratorów ról uprzywilejowanych, który umożliwia m.in. zarządzanie przypisaniami ról, zmienianie ustawień aktywacji roli i rozpoczynanie przeglądów dostępu.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-129">**Azure AD Directory Roles** located under the 'Manage' section is the dashboard for privileged role admins to manage role assignments, change role activation settings, start access reviews, and more.</span></span> <span data-ttu-id="ff7e9-130">Opcje na tym pulpicie nawigacyjnym są wyłączone dla każdego, kto nie jest administratorem roli uprzywilejowanej.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-130">The options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff7e9-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff7e9-131">Next steps</span></span>
<span data-ttu-id="ff7e9-132">Temat [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) (Omówienie aplikacji Azure AD Privileged Identity Management) zawiera więcej informacji dotyczących zarządzania dostępem administracyjnym w organizacji.</span><span class="sxs-lookup"><span data-stu-id="ff7e9-132">The [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
