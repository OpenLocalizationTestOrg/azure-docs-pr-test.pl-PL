---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy Autotask | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Autotask w miejscu pracy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 45130162271b20860607497ff93c6a668c415233
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="f9140-103">Samouczek: Integracji Azure Active Directory z Autotask w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="f9140-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="f9140-104">Z tego samouczka dowiesz się integrowanie Autotask miejsca pracy z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f9140-104">In this tutorial, you learn how to integrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9140-105">Integrowanie Autotask miejsca pracy z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f9140-105">Integrating Autotask Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9140-106">Można kontrolować w usłudze Azure AD, który ma dostęp do miejsca pracy Autotask</span><span class="sxs-lookup"><span data-stu-id="f9140-106">You can control in Azure AD who has access to Autotask Workplace</span></span>
- <span data-ttu-id="f9140-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Autotask w miejscu pracy (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9140-107">You can enable your users to automatically get signed-on to Autotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9140-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f9140-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f9140-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9140-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9140-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9140-110">Prerequisites</span></span>

<span data-ttu-id="f9140-111">Aby skonfigurować integrację usługi Azure AD z miejsca pracy Autotask, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f9140-111">To configure Azure AD integration with Autotask Workplace, you need the following items:</span></span>

- <span data-ttu-id="f9140-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9140-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9140-113">Obszar roboczy Autotask jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f9140-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="f9140-114">Musi być administratora lub administratora administrator w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="f9140-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="f9140-115">Musisz mieć konto administratora w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9140-115">You must have an administrator account in the Azure AD.</span></span>
- <span data-ttu-id="f9140-116">Użytkownicy, którzy będą korzystać z tej funkcji, muszą mieć konta w miejscu pracy i Azure AD, a ich adresów e-mail, oba muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="f9140-116">The users that will utilize this feature must have accounts within Workplace and the Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="f9140-117">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f9140-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9140-118">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f9140-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9140-119">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f9140-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f9140-120">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9140-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9140-121">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f9140-121">Scenario description</span></span>
<span data-ttu-id="f9140-122">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f9140-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9140-123">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f9140-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9140-124">Dodawanie miejsca pracy Autotask z galerii</span><span class="sxs-lookup"><span data-stu-id="f9140-124">Adding Autotask Workplace from the gallery</span></span>
2. <span data-ttu-id="f9140-125">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f9140-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-the-gallery"></a><span data-ttu-id="f9140-126">Dodawanie miejsca pracy Autotask z galerii</span><span class="sxs-lookup"><span data-stu-id="f9140-126">Adding Autotask Workplace from the gallery</span></span>
<span data-ttu-id="f9140-127">Aby skonfigurować integrację usługi Azure AD Autotask w miejscu pracy, należy dodać Autotask miejsca pracy z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f9140-127">To configure the integration of Autotask Workplace into Azure AD, you need to add Autotask Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9140-128">**Aby dodać miejsce pracy Autotask z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f9140-128">**To add Autotask Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9140-129">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f9140-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="f9140-131">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f9140-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f9140-132">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f9140-132">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="f9140-134">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f9140-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="f9140-136">W polu wyszukiwania wpisz **pracy Autotask**, wybierz pozycję **Autotask w miejscu pracy** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f9140-136">In the search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button to add the application.</span></span>

    ![Obszar roboczy Autotask na liście wyników](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f9140-138">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f9140-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f9140-139">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z miejsca pracy Autotask oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="f9140-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f9140-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w miejscu pracy Autotask jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9140-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask Workplace is to a user in Azure AD.</span></span> <span data-ttu-id="f9140-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w miejscu pracy Autotask musi określone.</span><span class="sxs-lookup"><span data-stu-id="f9140-141">In other words, a link relationship between an Azure AD user and the related user in Autotask Workplace needs to be established.</span></span>

<span data-ttu-id="f9140-142">W obszarze roboczym Autotask, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f9140-142">In Autotask Workplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f9140-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z miejsca pracy Autotask, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f9140-143">To configure and test Azure AD single sign-on with Autotask Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9140-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f9140-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9140-145">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f9140-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9140-146">**[Tworzenie użytkownika testowego pracy Autotask](#create-an-autotask-workplace-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Autotask miejsca pracy, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f9140-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask Workplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f9140-147">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f9140-147">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9140-148">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f9140-148">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f9140-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f9140-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f9140-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w miejscu pracy Autotask aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f9140-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="f9140-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z miejsca pracy Autotask, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f9140-151">**To configure Azure AD single sign-on with Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="f9140-152">W portalu Azure na **pracy Autotask** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f9140-152">In the Azure portal, on the **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="f9140-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f9140-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="f9140-156">Jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb, wykonaj następujące czynności na **Autotask Dołączanie domeny i adres URL** sekcji:</span><span class="sxs-lookup"><span data-stu-id="f9140-156">If you wish to configure the application in **IDP** initiated mode, perform the following steps on the **Autotask Workplace Domain and URLs** section:</span></span>

    ![Dołączanie Autotask domeny i adres URL pojedynczego logowania jednokrotnego informacje dotyczące IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="f9140-158">a.</span><span class="sxs-lookup"><span data-stu-id="f9140-158">a.</span></span> <span data-ttu-id="f9140-159">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="f9140-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="f9140-160">b.</span><span class="sxs-lookup"><span data-stu-id="f9140-160">b.</span></span> <span data-ttu-id="f9140-161">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="f9140-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="f9140-162">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane trybie wyboru **Pokaż zaawansowane ustawienia adresu URL** i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f9140-162">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following steps:</span></span>

    ![Dołączanie Autotask domeny i adres URL pojedynczego logowania jednokrotnego informacje dotyczące SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="f9140-164">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="f9140-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="f9140-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f9140-165">These values are not real.</span></span> <span data-ttu-id="f9140-166">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f9140-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f9140-167">Skontaktuj się z [zespołem pomocy technicznej Autotask miejsca pracy klienta](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="f9140-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get these values.</span></span> 

5. <span data-ttu-id="f9140-168">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f9140-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="f9140-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f9140-170">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f9140-172">W oknie przeglądarki innej witryny sieci web należy zalogować się do miejsca pracy Online przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="f9140-172">In a different web browser window, Log in to Workplace Online using the administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="f9140-173">Konfigurując IdP poddomeny będzie trzeba określić.</span><span class="sxs-lookup"><span data-stu-id="f9140-173">When configuring the IdP, a subdomain will need to be specified.</span></span> <span data-ttu-id="f9140-174">Aby potwierdzić prawidłowe poddomeny, zaloguj się do pracy w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="f9140-174">To confirm the correct subdomain, login to Workplace Online.</span></span> <span data-ttu-id="f9140-175">Po zalogowaniu, zwróć uwagę na poddomeny w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="f9140-175">Once logged in, make note to the subdomain in the URL.</span></span>
    ><span data-ttu-id="f9140-176">Należy nam, Europa, urząd certyfikacji lub Australia poddomeny i należy do zakresu od "https://" i ".awp.autotask.net/".</span><span class="sxs-lookup"><span data-stu-id="f9140-176">The subdomain is the part between the “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="f9140-177">Przejdź do **konfiguracji** > **rejestracji jednokrotnej** i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f9140-177">Go to **Configuration** > **Single Sign-On** and perform the following steps:</span></span>

    ![Jednym Autotask logowania jednokrotnego konfiguracji](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="f9140-179">a.</span><span class="sxs-lookup"><span data-stu-id="f9140-179">a.</span></span> <span data-ttu-id="f9140-180">Wybierz **pliku metadanych XML** opcji, a następnie przekaż **XML metadanych** pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f9140-180">Select the **XML Metadata File** option, and then upload the **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="f9140-181">b.</span><span class="sxs-lookup"><span data-stu-id="f9140-181">b.</span></span> <span data-ttu-id="f9140-182">Kliknij przycisk **włączenia funkcji logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="f9140-182">Click **Enable SSO**.</span></span>
    
    ![Autotask jednokrotnej Zatwierdzanie konfiguracji](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="f9140-184">c.</span><span class="sxs-lookup"><span data-stu-id="f9140-184">c.</span></span> <span data-ttu-id="f9140-185">Wybierz **potwierdzam, te informacje są poprawne i można zaufać tym IdP** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="f9140-185">Select the **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="f9140-186">d.</span><span class="sxs-lookup"><span data-stu-id="f9140-186">d.</span></span> <span data-ttu-id="f9140-187">Kliknij przycisk **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="f9140-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="f9140-188">Jeśli potrzebujesz pomocy przy konfigurowaniu Autotask w miejscu pracy, zobacz [tej strony](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) Aby uzyskać pomoc dotyczącą konta firmowego.</span><span class="sxs-lookup"><span data-stu-id="f9140-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="f9140-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f9140-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f9140-190">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f9140-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f9140-191">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f9140-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f9140-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9140-192">Create an Azure AD test user</span></span>

<span data-ttu-id="f9140-193">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f9140-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="f9140-195">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f9140-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9140-196">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f9140-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f9140-198">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f9140-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f9140-200">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f9140-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f9140-202">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f9140-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f9140-204">a.</span><span class="sxs-lookup"><span data-stu-id="f9140-204">a.</span></span> <span data-ttu-id="f9140-205">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9140-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9140-206">b.</span><span class="sxs-lookup"><span data-stu-id="f9140-206">b.</span></span> <span data-ttu-id="f9140-207">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f9140-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f9140-208">c.</span><span class="sxs-lookup"><span data-stu-id="f9140-208">c.</span></span> <span data-ttu-id="f9140-209">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="f9140-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f9140-210">d.</span><span class="sxs-lookup"><span data-stu-id="f9140-210">d.</span></span> <span data-ttu-id="f9140-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f9140-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="f9140-212">Tworzenie użytkownika testowego Autotask w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="f9140-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="f9140-213">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Autotask.</span><span class="sxs-lookup"><span data-stu-id="f9140-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="f9140-214">We współpracy z [Autotask pracy zespołu pomocy technicznej](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) Aby dodać użytkowników do miejsca pracy Autotask platformy.</span><span class="sxs-lookup"><span data-stu-id="f9140-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask Workplace platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f9140-215">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9140-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="f9140-216">W tej sekcji musisz włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do miejsca pracy Autotask.</span><span class="sxs-lookup"><span data-stu-id="f9140-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Autotask Workplace.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="f9140-218">**Aby przypisać Simona Britta Autotask w miejscu pracy, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f9140-218">**To assign Britta Simon to Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="f9140-219">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f9140-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f9140-221">Na liście aplikacji zaznacz **pracy Autotask**.</span><span class="sxs-lookup"><span data-stu-id="f9140-221">In the applications list, select **Autotask Workplace**.</span></span>

    ![Łącze Autotask w miejscu pracy na liście aplikacji](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="f9140-223">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f9140-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="f9140-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f9140-225">Click **Add** button.</span></span> <span data-ttu-id="f9140-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f9140-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="f9140-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f9140-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f9140-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f9140-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9140-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f9140-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f9140-231">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f9140-231">Test single sign-on</span></span>

<span data-ttu-id="f9140-232">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f9140-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f9140-233">Po kliknięciu kafelka Autotask w miejscu pracy, w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do miejsca pracy Autotask aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f9140-233">When you click the Autotask Workplace tile in the Access Panel, you should get automatically signed-on to your Autotask Workplace application.</span></span>
<span data-ttu-id="f9140-234">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f9140-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9140-235">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f9140-235">Additional resources</span></span>

* [<span data-ttu-id="f9140-236">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9140-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9140-237">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f9140-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

