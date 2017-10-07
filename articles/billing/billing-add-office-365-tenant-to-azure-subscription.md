---
title: "aaaUse usługi Office 365 dzierżawcy z subskrypcją platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooan katalogu (dzierżawcy) tooadd usługi Office 365 subskrypcji platformy Azure."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="f2741-103">Skojarz tooan dzierżawy usługi Office 365 subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f2741-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="f2741-104">Połącz oddzielne subskrypcji platformy Azure i usługi Office 365, umożliwiając dostęp do dzierżawy usługi Office 365 hello z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f2741-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="f2741-105">toolink subskrypcji, zaloguj się tooAzure z hello konta administratora usługi Azure, dodanie katalogu i Dodaj dzierżawy usługi Azure Active Directory toohello konta organizacyjne hello usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="f2741-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="f2741-106">Jeśli chcesz subskrypcji usługi Office 365 dla użytkowników w wystąpieniu usługi Azure Active Directory lub mieć konto usługi Office 365, ale nie jest konto platformy Azure, zobacz [tworzenia konta platformy Azure z kontem usługi Office 365](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="f2741-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f2741-107">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="f2741-107">Before you begin</span></span>
* <span data-ttu-id="f2741-108">Musi mieć hello poświadczenia administratora usługi subskrypcji platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f2741-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="f2741-109">Konta administratora współpracującego nie można wykonać niektóre kroki hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="f2741-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="f2741-110">toochange administratorem usługi, zobacz [jak tooadd lub zmień role administratora platformy Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="f2741-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="f2741-111">Musi mieć poświadczenia administratora globalnego dzierżawy usługi Office 365 hello hello.</span><span class="sxs-lookup"><span data-stu-id="f2741-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="f2741-112">adres e-mail administratora usługi hello Hello nie może występować w hello dzierżawy usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="f2741-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="f2741-113">adres e-mail administratora usługi hello Hello musi niezgodne z administratorami globalnymi dzierżawy hello usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="f2741-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="f2741-114">Jeśli używany jest adres e-mail konta Microsoft i konta organizacyjnego, tymczasowo zmienić administratora usługi hello toouse Twojej subskrypcji platformy Azure innego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f2741-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="f2741-115">Możesz utworzyć konto Microsoft na powitania [strony Rejestracja konta Microsoft](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="f2741-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="f2741-116">Łączenie subskrypcji tooAzure dzierżawy usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="f2741-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="f2741-117">toohello dzierżawy usługi Office 365 hello tooassociate subskrypcji platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f2741-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="f2741-118">Krok 1: Dodaj tooyour dzierżawy usługi Office 365 subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f2741-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="f2741-119">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) przy użyciu poświadczeń administratora usługi hello.</span><span class="sxs-lookup"><span data-stu-id="f2741-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Zrzut ekranu Azure logowanie](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="f2741-121">Wybierz w okienku po lewej stronie powitania **usługi ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="f2741-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="f2741-122">Niepowołanymi dzierżawy hello usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="f2741-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="f2741-123">Jeśli zostanie wyświetlony, Pomiń zbyt[krok 2: Zmień katalog hello skojarzone z hello subskrypcji platformy Azure](#Step2).</span><span class="sxs-lookup"><span data-stu-id="f2741-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Wpis zrzut ekranu z usługi Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="f2741-125">Wybierz **nowy** > **katalogu** > **tworzenie NIESTANDARDOWYCH**.</span><span class="sxs-lookup"><span data-stu-id="f2741-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Utwórz niestandardowy zrzut ekranu z usługą Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="f2741-127">Na powitania **Dodaj katalog** w obszarze **katalogu**, wybierz pozycję **Użyj istniejącego katalogu**.</span><span class="sxs-lookup"><span data-stu-id="f2741-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="f2741-128">Następnie wybierz **jestem toobe gotowa, teraz wylogować**i wybierz **Complete** ![ukończyć ikona](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="f2741-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Zrzut ekranu przedstawiający "Użyj istniejącego katalogu"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="f2741-130">Po zarejestrowaniu zalogować się przy użyciu poświadczeń administratora globalnego hello dzierżawy usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="f2741-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Logowanie administratora globalnego zrzut ekranu usługi Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="f2741-132">Wybierz **kontynuować**.</span><span class="sxs-lookup"><span data-stu-id="f2741-132">Select **Continue**.</span></span>
   
    ![Zrzut ekranu przedstawiający weryfikacji](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="f2741-134">Wybierz **Wyloguj się teraz**.</span><span class="sxs-lookup"><span data-stu-id="f2741-134">Select **Sign out now**.</span></span>
   
    ![Zrzut ekranu przedstawiający wylogowania](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="f2741-136">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) przy użyciu poświadczeń administratora usługi hello.</span><span class="sxs-lookup"><span data-stu-id="f2741-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Zrzut ekranu Azure logowanie](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="f2741-138">Dzierżawy usługi Office 365 na pulpicie nawigacyjnym hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="f2741-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![Zrzut ekranu przedstawiający pulpit nawigacyjny](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="f2741-140"><a name="Step2"></a>Krok 2: Zmień katalog hello skojarzony z hello subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f2741-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="f2741-141">Wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="f2741-141">Select **Settings**.</span></span>
   
    ![Zrzut ekranu Azure ikona klasycznych ustawień portalu](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="f2741-143">Wybierz subskrypcję platformy Azure, a następnie wybierz **Edytuj katalog**.</span><span class="sxs-lookup"><span data-stu-id="f2741-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Zrzut ekranu Azure subskrypcji edycji katalogu](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="f2741-145">Wybierz **dalej** ![dalej](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="f2741-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Zrzut ekranu przedstawiający "Zmiany hello skojarzone katalogu"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="f2741-147">Przejrzyj kont hello, których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="f2741-147">Review hello affected accounts.</span></span> <span data-ttu-id="f2741-148">W przypadku wszystkich administratorów wspólnej i [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) użytkownicy z dostępem przypisane w hello istniejących grup zasobów zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="f2741-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="f2741-149">Ostrzeżenie Hello, które otrzymujesz wymienia tylko usunięcie hello współadministratorów.</span><span class="sxs-lookup"><span data-stu-id="f2741-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![Zrzut ekranu pokazujący hello kont administratora współpracującego toobe usunięte.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Zrzut ekranu przedstawia przykład toobe konta użytkownika usunięte.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="f2741-152">Wybierz **Complete** ![ukończyć ikona](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="f2741-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="f2741-153">Krok 3: Dodawanie konta organizacyjnego usługi Office 365 jako dzierżawy usługi Azure Active Directory toohello współadministratorów</span><span class="sxs-lookup"><span data-stu-id="f2741-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="f2741-154">Wybierz hello **ADMINISTRATORZY** , a następnie wybierz **dodać**.</span><span class="sxs-lookup"><span data-stu-id="f2741-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Karta Administratorzy ustawienia portalu klasycznego zrzut ekranu Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="f2741-156">Wprowadź konto organizacyjne dzierżawy usługi Office 365, wybierz hello subskrypcji platformy Azure, a następnie wybierz **Complete** ![ukończyć ikona](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="f2741-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Zrzut ekranu Azure Dodaj współadministratorem — okno dialogowe](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="f2741-158">Przejdź wstecz toohello **ADMINISTRATORZY** kartę. Witaj konta organizacyjnego wyświetlany jako współadministrator powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="f2741-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![Zrzut ekranu przedstawiający kartę Administratorzy](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="f2741-160">Test tooAzure dostępu z kontem administratora współpracującego hello.</span><span class="sxs-lookup"><span data-stu-id="f2741-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="f2741-161">a.</span><span class="sxs-lookup"><span data-stu-id="f2741-161">a.</span></span> <span data-ttu-id="f2741-162">Wyloguj hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f2741-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="f2741-163">b.</span><span class="sxs-lookup"><span data-stu-id="f2741-163">b.</span></span> <span data-ttu-id="f2741-164">Otwórz hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f2741-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="f2741-165">c.</span><span class="sxs-lookup"><span data-stu-id="f2741-165">c.</span></span> <span data-ttu-id="f2741-166">Wprowadź poświadczenia administratora współpracującego hello hello, a następnie wybierz **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="f2741-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Zrzut ekranu Azure strony logowania](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="f2741-168">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="f2741-168">Need help?</span></span> <span data-ttu-id="f2741-169">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="f2741-169">Contact support.</span></span>
<span data-ttu-id="f2741-170">Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="f2741-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


