---
title: "Samouczek: Integracji Azure Active Directory z przyjęcia LMS | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i przyjęcia LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 3c68c3ac7d6be593476d419f8c015931b206eead
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="9b517-103">Samouczek: Integracji Azure Active Directory z przyjęcia LMS</span><span class="sxs-lookup"><span data-stu-id="9b517-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="9b517-104">Z tego samouczka dowiesz się integrowanie LMS przyjęcia w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b517-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b517-105">Integracja z usługą Azure AD przyjęcia LMS zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9b517-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9b517-106">Można kontrolować w usłudze Azure AD, który ma dostęp do przyjęcia LMS</span><span class="sxs-lookup"><span data-stu-id="9b517-106">You can control in Azure AD who has access to Absorb LMS</span></span>
- <span data-ttu-id="9b517-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do przyjęcia LMS (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b517-107">You can enable your users to automatically get signed-on to Absorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b517-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9b517-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9b517-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="9b517-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9b517-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9b517-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b517-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9b517-111">Prerequisites</span></span>

<span data-ttu-id="9b517-112">Aby skonfigurować integrację usługi Azure AD z przyjęcia LMS, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9b517-112">To configure Azure AD integration with Absorb LMS, you need the following items:</span></span>

- <span data-ttu-id="9b517-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b517-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9b517-114">Przyjęcia LMS jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9b517-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b517-115">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9b517-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b517-116">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9b517-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b517-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9b517-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b517-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b517-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b517-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9b517-119">Scenario description</span></span>
<span data-ttu-id="9b517-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9b517-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b517-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9b517-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b517-122">Dodawanie przyjęcia LMS z galerii</span><span class="sxs-lookup"><span data-stu-id="9b517-122">Adding Absorb LMS from the gallery</span></span>
2. <span data-ttu-id="9b517-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9b517-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-the-gallery"></a><span data-ttu-id="9b517-124">Dodawanie przyjęcia LMS z galerii</span><span class="sxs-lookup"><span data-stu-id="9b517-124">Adding Absorb LMS from the gallery</span></span>
<span data-ttu-id="9b517-125">Aby skonfigurować integrację przyjęcia LMS w usłudze Azure AD, należy dodać przyjęcia LMS z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9b517-125">To configure the integration of Absorb LMS in to Azure AD, you need to add Absorb LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9b517-126">**Aby dodać przyjęcia LMS z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9b517-126">**To add Absorb LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9b517-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9b517-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="9b517-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9b517-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9b517-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9b517-130">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="9b517-132">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b517-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="9b517-134">W polu wyszukiwania wpisz **przyjęcia LMS**, wybierz pozycję **przyjęcia LMS** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9b517-134">In the search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button to add the application.</span></span>

    ![Przyjęcia LMS na liście wyników](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9b517-136">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9b517-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9b517-137">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9b517-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9b517-138">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w przyjęcia LMS jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b517-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Absorb LMS is to a user in Azure AD.</span></span> <span data-ttu-id="9b517-139">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w przyjęcia LMS musi się.</span><span class="sxs-lookup"><span data-stu-id="9b517-139">In other words, a link relationship between an Azure AD user and the related user in Absorb LMS needs to be established.</span></span>

<span data-ttu-id="9b517-140">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w LMS przyjęcia.</span><span class="sxs-lookup"><span data-stu-id="9b517-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Absorb LMS.</span></span>

<span data-ttu-id="9b517-141">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9b517-141">To configure and test Azure AD single sign-on with Absorb LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9b517-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9b517-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9b517-143">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b517-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b517-144">**[Tworzenie użytkownika testowego przyjęcia LMS](#create-an-absorb-lms-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta przyjęcia LMS połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9b517-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - to have a counterpart of Britta Simon in Absorb LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9b517-145">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9b517-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b517-146">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9b517-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9b517-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9b517-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9b517-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji LMS przyjęcia.</span><span class="sxs-lookup"><span data-stu-id="9b517-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="9b517-149">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9b517-149">**To configure Azure AD single sign-on with Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="9b517-150">W portalu Azure na **przyjęcia LMS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9b517-150">In the Azure portal, on the **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="9b517-152">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9b517-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="9b517-154">Na **adresy URL i przyjęcia domeny LMS** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9b517-154">On the **Absorb LMS Domain and URLs** section, perform the following steps:</span></span>

    ![Przyjęcia LMS domeny i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="9b517-156">a.</span><span class="sxs-lookup"><span data-stu-id="9b517-156">a.</span></span> <span data-ttu-id="9b517-157">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="9b517-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="9b517-158">b.</span><span class="sxs-lookup"><span data-stu-id="9b517-158">b.</span></span> <span data-ttu-id="9b517-159">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="9b517-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9b517-160">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="9b517-160">These values are not the real.</span></span> <span data-ttu-id="9b517-161">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="9b517-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9b517-162">Skontaktuj się z [zespołem pomocy technicznej klienta LMS przyjęcia](https://www.absorblms.com/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="9b517-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) to get these values.</span></span> 

4. <span data-ttu-id="9b517-163">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9b517-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="9b517-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9b517-165">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9b517-167">Na **przyjęcia konfiguracji LMS** , kliknij przycisk **skonfigurować LMS przyjęcia** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9b517-167">On the **Absorb LMS Configuration** section, click **Configure Absorb LMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9b517-168">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9b517-168">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Przyjęcia LMS konfiguracji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="9b517-170">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do przyjęcia LMS witryny firmy.</span><span class="sxs-lookup"><span data-stu-id="9b517-170">In a different web browser window, log in to your Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="9b517-171">Kliknij przycisk **ikonę konta** w interfejsie administratora.</span><span class="sxs-lookup"><span data-stu-id="9b517-171">Click the **Account Icon** on the admin interface.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="9b517-173">Kliknij przycisk **ustawienia portalu**.</span><span class="sxs-lookup"><span data-stu-id="9b517-173">Click **Portal Settings**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="9b517-175">Kliknij przycisk **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="9b517-175">Click the **Users** tab.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="9b517-177">Wykonaj poniższe kroki, aby uzyskać dostępu do pola konfiguracji rejestracji jednokrotnej:</span><span class="sxs-lookup"><span data-stu-id="9b517-177">Perform the following steps to access the Single Sign-On configuration fields:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="9b517-179">a.</span><span class="sxs-lookup"><span data-stu-id="9b517-179">a.</span></span> <span data-ttu-id="9b517-180">Wybierz odpowiednie **tryb**.</span><span class="sxs-lookup"><span data-stu-id="9b517-180">Select the appropriate **Mode**.</span></span>

    <span data-ttu-id="9b517-181">b.</span><span class="sxs-lookup"><span data-stu-id="9b517-181">b.</span></span> <span data-ttu-id="9b517-182">Usuń certyfikat został już pobrany z portalu Azure w programie Notatnik Otwórz **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---** tag, a następnie wklej zawartość pozostałych **klucza** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9b517-182">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Key** textbox.</span></span>
    
    <span data-ttu-id="9b517-183">c.</span><span class="sxs-lookup"><span data-stu-id="9b517-183">c.</span></span> <span data-ttu-id="9b517-184">W **właściwość identyfikatora**, wybierz odpowiedni atrybut, który skonfigurowano jako identyfikator użytkownika w usłudze Azure AD (na przykład, jeśli wybrano userprinciplename w usłudze Azure AD, a następnie zaznaczony tutaj nazwę użytkownika.)</span><span class="sxs-lookup"><span data-stu-id="9b517-184">In the **Id Property**, select the appropriate attribute which you have configured as the user identifier in the Azure AD (For example, If the userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="9b517-185">d.</span><span class="sxs-lookup"><span data-stu-id="9b517-185">d.</span></span> <span data-ttu-id="9b517-186">W **adres URL logowania**, Wklej **"SAML pojedynczy znak na adres URL usługi"** wartość została skopiowana z **Konfigurowanie logowania jednokrotnego** okna portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9b517-186">In the **Login URL**, paste the **“SAML Single Sign-On Service URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="9b517-187">e.</span><span class="sxs-lookup"><span data-stu-id="9b517-187">e.</span></span> <span data-ttu-id="9b517-188">W **adresu URL wylogowania**, Wklej **"Adres URL Sign-Out"** wartość została skopiowana z **Konfigurowanie logowania jednokrotnego** okna portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9b517-188">In the **Logout URL**, paste the **“Sign-Out URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

13. <span data-ttu-id="9b517-189">Włącz **"Zezwalaj tylko na logowanie SSO"**.</span><span class="sxs-lookup"><span data-stu-id="9b517-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="9b517-191">Kliknij przycisk **"Zapisz".**</span><span class="sxs-lookup"><span data-stu-id="9b517-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="9b517-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9b517-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9b517-193">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9b517-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9b517-194">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b517-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9b517-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b517-195">Create an Azure AD test user</span></span>

<span data-ttu-id="9b517-196">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b517-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="9b517-198">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9b517-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9b517-199">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9b517-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9b517-201">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9b517-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9b517-203">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b517-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9b517-205">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9b517-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b517-207">a.</span><span class="sxs-lookup"><span data-stu-id="9b517-207">a.</span></span> <span data-ttu-id="9b517-208">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b517-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b517-209">b.</span><span class="sxs-lookup"><span data-stu-id="9b517-209">b.</span></span> <span data-ttu-id="9b517-210">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9b517-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b517-211">c.</span><span class="sxs-lookup"><span data-stu-id="9b517-211">c.</span></span> <span data-ttu-id="9b517-212">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9b517-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9b517-213">d.</span><span class="sxs-lookup"><span data-stu-id="9b517-213">d.</span></span> <span data-ttu-id="9b517-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9b517-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="9b517-215">Tworzenie użytkownika testowego przyjęcia LMS</span><span class="sxs-lookup"><span data-stu-id="9b517-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="9b517-216">Aby umożliwić użytkownikom usługi Azure AD zalogować się do przyjęcia LMS, ich należy udostępnić w celu przyjęcia LMS.</span><span class="sxs-lookup"><span data-stu-id="9b517-216">To enable Azure AD users to log in to Absorb LMS, they must be provisioned in to Absorb LMS.</span></span>  
<span data-ttu-id="9b517-217">W przypadku przyjęcia LMS inicjowania obsługi administracyjnej jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="9b517-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="9b517-218">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9b517-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9b517-219">Zaloguj się do witryny firmy przyjęcia LMS jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9b517-219">Log in to your Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="9b517-220">Kliknij przycisk **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="9b517-220">Click **Users** tab.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="9b517-222">Kliknij przycisk **użytkowników** w obszarze **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="9b517-222">Click **Users** under the **Users** tab.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="9b517-224">Wybierz **użytkownika** z **Dodaj nowy** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="9b517-224">Select **User** from **Add New** drop-down.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="9b517-226">Na **Dodaj użytkownika** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9b517-226">On the **Add User** page, perform the following steps:</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="9b517-228">a.</span><span class="sxs-lookup"><span data-stu-id="9b517-228">a.</span></span> <span data-ttu-id="9b517-229">W **imię** pole tekstowe, nazwa typu pierwszy, takich jak Britta.</span><span class="sxs-lookup"><span data-stu-id="9b517-229">In the **First Name** textbox, type the first name like Britta.</span></span>

    <span data-ttu-id="9b517-230">b.</span><span class="sxs-lookup"><span data-stu-id="9b517-230">b.</span></span> <span data-ttu-id="9b517-231">W **nazwisko** tekstowym, wpisz nazwisko, takich jak Simona.</span><span class="sxs-lookup"><span data-stu-id="9b517-231">In the **Last Name** textbox, type the last name like Simon.</span></span>
    
    <span data-ttu-id="9b517-232">c.</span><span class="sxs-lookup"><span data-stu-id="9b517-232">c.</span></span> <span data-ttu-id="9b517-233">W **Username** tekstowym, wpisz nazwę użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b517-233">In the **Username** textbox, type the user name like Britta Simon.</span></span>

    <span data-ttu-id="9b517-234">d.</span><span class="sxs-lookup"><span data-stu-id="9b517-234">d.</span></span> <span data-ttu-id="9b517-235">W **hasło** tekstowym, wpisz hasło Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b517-235">In the **Password** textbox, type the password of Britta Simon.</span></span>

    <span data-ttu-id="9b517-236">e.</span><span class="sxs-lookup"><span data-stu-id="9b517-236">e.</span></span> <span data-ttu-id="9b517-237">W **Potwierdź hasło** tekstowym, wpisz to samo hasło.</span><span class="sxs-lookup"><span data-stu-id="9b517-237">In the **Confirm Password** textbox, type the same password.</span></span>
    
    <span data-ttu-id="9b517-238">f.</span><span class="sxs-lookup"><span data-stu-id="9b517-238">f.</span></span> <span data-ttu-id="9b517-239">Należy go jako **ACTIVE**.</span><span class="sxs-lookup"><span data-stu-id="9b517-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="9b517-240">Kliknij przycisk **"Zapisz".**</span><span class="sxs-lookup"><span data-stu-id="9b517-240">Click **"Save."**</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9b517-241">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b517-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="9b517-242">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do przyjęcia LMS.</span><span class="sxs-lookup"><span data-stu-id="9b517-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span></span>

![Przypisanie roli użytkownika][200]

<span data-ttu-id="9b517-244">**Aby przypisać Simona Britta do przyjęcia LMS, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9b517-244">**To assign Britta Simon to Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="9b517-245">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9b517-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9b517-247">Na liście aplikacji zaznacz **przyjęcia LMS**.</span><span class="sxs-lookup"><span data-stu-id="9b517-247">In the applications list, select **Absorb LMS**.</span></span>

    ![Łącze przyjęcia LMS na liście aplikacji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="9b517-249">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9b517-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="9b517-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9b517-251">Click **Add** button.</span></span> <span data-ttu-id="9b517-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b517-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="9b517-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9b517-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9b517-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b517-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b517-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b517-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9b517-257">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9b517-257">Test single sign-on</span></span>

<span data-ttu-id="9b517-258">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9b517-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9b517-259">Kliknij Kafelek LMS przyjęcia w panelu dostępu, użytkownik będzie uzyskać automatycznie zalogowane do przyjęcia LMS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b517-259">Click the Absorb LMS tile in the Access Panel, you will get automatically signed-on to your Absorb LMS application.</span></span> <span data-ttu-id="9b517-260">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9b517-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9b517-261">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9b517-261">Additional resources</span></span>

* [<span data-ttu-id="9b517-262">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b517-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b517-263">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9b517-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

