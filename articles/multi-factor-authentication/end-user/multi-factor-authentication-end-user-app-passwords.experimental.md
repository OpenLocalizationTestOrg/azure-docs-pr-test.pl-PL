---
title: "toouse aaaHow haseł aplikacji w usłudze Azure MFA? | Microsoft Docs"
description: "Ta strona będzie pomaganie użytkownikom w zrozumieniu hasła aplikacji są i jakie są używane dla z uwzględnieniem tooAzure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="42c41-104">Co to są hasła aplikacji w usłudze Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="42c41-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="42c41-105">Niektóre aplikacje korzystające z przeglądarki, takie jak hello klienta natywnego poczty e-mail firmy Apple, który używa programu Exchange Active Sync aktualnie nie obsługują uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="42c41-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="42c41-106">Uwierzytelnianie wieloskładnikowe jest włączone dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42c41-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="42c41-107">To oznacza, że użytkownik nie może używać uwierzytelniania wieloskładnikowego jeśli:</span><span class="sxs-lookup"><span data-stu-id="42c41-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="42c41-108">włączono Hello użytkownika usługi Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="42c41-108">hello user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="42c41-109">Witaj użytkownik próbuje toouse aplikacji korzystających z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="42c41-109">hello user is trying toouse a non-browser app.</span></span>

<span data-ttu-id="42c41-110">Hasła aplikacji, dzięki czemu hello użytkownika toouse hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42c41-110">An app password allows hello user toouse hello app.</span></span>

<span data-ttu-id="42c41-111">Po utworzeniu haseł aplikacji, użyj zamiast oryginalnemu hasłu z tych aplikacji korzystających z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="42c41-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="42c41-112">Podczas rejestrowania na potrzeby weryfikacji dwuetapowej, jeśli nie mogą również wykonywać weryfikacji drugi hello jest informuje Microsoft nie toolet zarejestrować każdy użytkownik się przy użyciu hasła.</span><span class="sxs-lookup"><span data-stu-id="42c41-112">When you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="42c41-113">powitania klienta natywnego poczty e-mail firmy Apple na telefonie nie można zalogować się jako użytkownik, ponieważ nie można żądać na potrzeby weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="42c41-113">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="42c41-114">Witaj rozwiązania problemu toothis jest toocreate bardziej bezpieczne hasło aplikacji, które nie są używane bieżące.</span><span class="sxs-lookup"><span data-stu-id="42c41-114">hello solution toothis problem is toocreate a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="42c41-115">Hasła aplikacji są tylko dla tych aplikacji, które nie obsługują weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="42c41-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="42c41-116">Użyj hasła aplikacji hello, dzięki czemu aplikacje mogą obejść usługę Multi-Factor authentication i kontynuować toowork.</span><span class="sxs-lookup"><span data-stu-id="42c41-116">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>


> [!NOTE]
> <span data-ttu-id="42c41-117">Klienci Office 2013 (w tym programu Outlook) obsługują nowe protokoły uwierzytelniania i może być używany z weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="42c41-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="42c41-118">Hasła aplikacji nie są wymagane do użytku z klientami pakietu Office 2013.</span><span class="sxs-lookup"><span data-stu-id="42c41-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="42c41-119">Aby uzyskać więcej informacji, zobacz [pakietu Office 2013 nowoczesnego uwierzytelniania anonsowania publicznej wersji](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="42c41-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="42c41-120">Jak toouse haseł aplikacji</span><span class="sxs-lookup"><span data-stu-id="42c41-120">How toouse app passwords</span></span>
<span data-ttu-id="42c41-121">Poniżej przedstawiono niektóre tooknow zagadnienia dotyczące haseł aplikacji:</span><span class="sxs-lookup"><span data-stu-id="42c41-121">Here are some things tooknow about app passwords:</span></span>

* <span data-ttu-id="42c41-122">Nie twórz haseł aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42c41-122">You don't create your own app passwords.</span></span> <span data-ttu-id="42c41-123">Są one automatycznie generowane.</span><span class="sxs-lookup"><span data-stu-id="42c41-123">They are automatically generated.</span></span>
* <span data-ttu-id="42c41-124">Obecnie istnieje limit 40 haseł na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42c41-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="42c41-125">Jeśli spróbujesz toocreate hasła aplikacji po osiągnięciu limitu hello, będziesz mieć toodelete istniejących haseł aplikacji przed utworzeniem nowego.</span><span class="sxs-lookup"><span data-stu-id="42c41-125">If you try toocreate an app password after you have reached hello limit, you'll have toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="42c41-126">Używanie jednego hasła aplikacji na urządzenie, nie na aplikację.</span><span class="sxs-lookup"><span data-stu-id="42c41-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="42c41-127">Na przykład można utworzyć hasło aplikacji dla komputera przenośnego i korzystać z dla wszystkich aplikacji na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="42c41-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="42c41-128">Następnie utwórz drugi toouse hasło aplikacji dla wszystkich aplikacji na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="42c41-128">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="42c41-129">Jeden hello hasła aplikacji są podane w pierwszym można zarejestrować na potrzeby weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="42c41-129">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="42c41-130">Jeśli potrzebujesz dodatkowych z nich, można je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="42c41-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="42c41-131">Tworzenie i usuwanie haseł aplikacji</span><span class="sxs-lookup"><span data-stu-id="42c41-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="42c41-132">Podczas początkowej logowanie są podane hasło aplikacji, które można użyć.</span><span class="sxs-lookup"><span data-stu-id="42c41-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="42c41-133">Można również tworzyć i Usuń hasła aplikacji w późniejszym czasie na.</span><span class="sxs-lookup"><span data-stu-id="42c41-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="42c41-134">Jak usunąć hasła aplikacji, zależy od tego, jak używasz usługi Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="42c41-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="42c41-135">Hello odpowiedzi następujące pytania dotyczące toodetermine, w której powinien przejść toomanage hasła aplikacji:</span><span class="sxs-lookup"><span data-stu-id="42c41-135">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="42c41-136">Używasz weryfikacji dwuetapowej dla swojego osobistego konta Microsoft?</span><span class="sxs-lookup"><span data-stu-id="42c41-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="42c41-137">Jeśli tak, należy zapoznać się toohello [haseł aplikacji i weryfikacji dwuetapowej](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artykułu, aby uzyskać pomoc.</span><span class="sxs-lookup"><span data-stu-id="42c41-137">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="42c41-138">Jeśli nie, nadal tooquestion dwa.</span><span class="sxs-lookup"><span data-stu-id="42c41-138">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="42c41-139">OK, aby używać weryfikację dwuetapową dla konta firmowego lub szkolnego.</span><span class="sxs-lookup"><span data-stu-id="42c41-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="42c41-140">Używasz go toosign w aplikacjach tooOffice 365?</span><span class="sxs-lookup"><span data-stu-id="42c41-140">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="42c41-141">Jeśli tak, należy zapoznać się zbyt[utworzyć hasło aplikacji dla usługi Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) Aby uzyskać pomoc.</span><span class="sxs-lookup"><span data-stu-id="42c41-141">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="42c41-142">Jeśli nie, nadal tooquestion trzech.</span><span class="sxs-lookup"><span data-stu-id="42c41-142">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="42c41-143">Używasz weryfikacji dwuetapowej platformie Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="42c41-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="42c41-144">Jeśli tak, kontynuuj toohello [zarządzać hasłami aplikacji w portalu Azure hello](#manage-app-passwords-in-the-Azure-portal) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="42c41-144">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="42c41-145">Jeśli nie, nadal tooquestion czterech.</span><span class="sxs-lookup"><span data-stu-id="42c41-145">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="42c41-146">Nie masz pewności, gdy używasz weryfikację dwuetapową?</span><span class="sxs-lookup"><span data-stu-id="42c41-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="42c41-147">Kontynuować toohello [Zarządzanie hasłami aplikacji z portalu MyApps hello](#manage-app-passwords-with-the-myapps-portal) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="42c41-147">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="42c41-148">Zarządzanie hasłami aplikacji w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="42c41-148">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="42c41-149">Korzystając z platformy Azure, weryfikację dwuetapową, ma toocreate hasła aplikacji za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="42c41-149">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="42c41-150">hasła aplikacji toocreate w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="42c41-150">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="42c41-151">Zaloguj się toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="42c41-151">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="42c41-152">U góry hello kliknij prawym przyciskiem myszy nazwę użytkownika, a następnie wybierz dodatkowa weryfikacja zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="42c41-152">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="42c41-153">Na stronie biurowego hello u góry hello zaznacz haseł aplikacji</span><span class="sxs-lookup"><span data-stu-id="42c41-153">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="42c41-154">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="42c41-154">Click **Create**.</span></span>
5. <span data-ttu-id="42c41-155">Wprowadź nazwę hasła aplikacji hello, a następnie kliknij przycisk **dalej**</span><span class="sxs-lookup"><span data-stu-id="42c41-155">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="42c41-156">Skopiuj Schowka toohello hasła aplikacji hello i wklej go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42c41-156">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![Chmura](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="42c41-158">hasła aplikacji toodelete w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="42c41-158">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="42c41-159">Zaloguj się toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="42c41-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="42c41-160">U góry hello kliknij prawym przyciskiem myszy nazwę użytkownika, a następnie wybierz dodatkowa weryfikacja zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="42c41-160">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="42c41-161">U góry hello, dalej tooadditional weryfikacji zabezpieczeń, wybierz **hasła aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="42c41-161">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="42c41-162">Dalej hasła aplikacji toohello ma toodelete, wybierz opcję **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="42c41-162">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="42c41-163">Potwierdź usunięcie hello klikając **tak**.</span><span class="sxs-lookup"><span data-stu-id="42c41-163">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="42c41-164">Po usunięciu hasła aplikacji hello, możesz kliknąć **zamknąć**.</span><span class="sxs-lookup"><span data-stu-id="42c41-164">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="42c41-165">Zarządzanie hasłami aplikacji hello MyApps Portal.</span><span class="sxs-lookup"><span data-stu-id="42c41-165">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="42c41-166">Jeśli nie masz pewności, jak używać usługi Multi-Factor authentication, następnie zawsze możesz utworzyć i usunąć hasła aplikacji za pośrednictwem portalu myapps hello.</span><span class="sxs-lookup"><span data-stu-id="42c41-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="42c41-167">hasła aplikacji przy użyciu toocreate hello Myapps portalu</span><span class="sxs-lookup"><span data-stu-id="42c41-167">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="42c41-168">Zaloguj się za[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="42c41-168">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="42c41-169">Kliknij swoją nazwę na powitania górnym rogu i wybierz polecenie **profilu**.</span><span class="sxs-lookup"><span data-stu-id="42c41-169">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="42c41-170">Wybierz **dodatkowej weryfikacji zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="42c41-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="42c41-171">![Wybierz opcję dodatkowa weryfikacja zabezpieczeń — zrzut ekranu](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="42c41-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="42c41-172">Wybierz **hasła aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="42c41-172">Select **app passwords**.</span></span>
   <span data-ttu-id="42c41-173">![Wybierz hasła aplikacji — zrzut ekranu](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="42c41-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="42c41-174">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="42c41-174">Click **Create**.</span></span>
6. <span data-ttu-id="42c41-175">Wprowadź nazwę hasła aplikacji hello, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="42c41-175">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="42c41-176">Skopiuj Schowka toohello hasła aplikacji hello i wklej go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42c41-176">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="42c41-177">![Utwórz hasło aplikacji](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="42c41-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="42c41-178">hasła aplikacji przy użyciu toodelete hello Myapps portalu</span><span class="sxs-lookup"><span data-stu-id="42c41-178">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="42c41-179">Zaloguj się za[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="42c41-179">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="42c41-180">U góry hello wybierz profil.</span><span class="sxs-lookup"><span data-stu-id="42c41-180">At hello top, select profile.</span></span>
3. <span data-ttu-id="42c41-181">Wybierz **dodatkowej weryfikacji zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="42c41-181">Select **Additional Security Verification**.</span></span>

   ![Wybierz opcję dodatkowa weryfikacja zabezpieczeń — zrzut ekranu](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="42c41-183">Wybierz **hasła aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="42c41-183">Select **app passwords**.</span></span>

   ![Wybierz hasła aplikacji — zrzut ekranu](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="42c41-185">Kliknij przycisk Dalej hasła aplikacji toohello ma toodelete, **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="42c41-185">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![Usuń hasło aplikacji](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="42c41-187">Upewnij się, że chcesz toodelete to hasło, klikając **tak**.</span><span class="sxs-lookup"><span data-stu-id="42c41-187">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="42c41-188">Po usunięciu hasła aplikacji hello, możesz kliknąć **zamknąć**.</span><span class="sxs-lookup"><span data-stu-id="42c41-188">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42c41-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42c41-189">Next steps</span></span>

- [<span data-ttu-id="42c41-190">Zarządzanie ustawieniami weryfikacji dwuetapowej</span><span class="sxs-lookup"><span data-stu-id="42c41-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="42c41-191">Wypróbuj hello [aplikacji Microsoft Authenticator](microsoft-authenticator-app-how-to.md) tooverify Twojego logowania z powiadomieniami aplikacji, nie odbiera teksty lub wywołań.</span><span class="sxs-lookup"><span data-stu-id="42c41-191">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
