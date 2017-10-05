---
title: "Samouczek: Integracji Azure Active Directory z MOVEit Transfer — integracji z usługą Azure AD | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i MOVEit Transfer — integracji z usługą Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: d35aceb9be2d0ff49f86a00cc84f5deb198d88f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="5795c-103">Samouczek: Integracji Azure Active Directory z MOVEit Transfer — integracji z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="5795c-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="5795c-104">Z tego samouczka dowiesz się integrowanie MOVEit Transfer — integracji z usługą Azure AD z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5795c-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5795c-105">Integrowanie MOVEit Transfer — integracji z usługą Azure AD z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5795c-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5795c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do transferu MOVEit - integracji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5795c-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="5795c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane transferem MOVEit - integracji usługi Azure AD (logowanie jednokrotne) z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5795c-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5795c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5795c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5795c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5795c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5795c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5795c-110">Prerequisites</span></span>

<span data-ttu-id="5795c-111">Aby skonfigurować integrację usługi Azure AD z MOVEit Transfer — integracji z usługą Azure AD, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5795c-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span></span>

- <span data-ttu-id="5795c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5795c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5795c-113">MOVEit Transfer — usługi Azure AD integracji jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5795c-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5795c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5795c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5795c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5795c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5795c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5795c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5795c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5795c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5795c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5795c-118">Scenario description</span></span>
<span data-ttu-id="5795c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5795c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5795c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5795c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5795c-121">Dodawanie MOVEit Transfer — integracji z usługą Azure AD z galerii</span><span class="sxs-lookup"><span data-stu-id="5795c-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
2. <span data-ttu-id="5795c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5795c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a><span data-ttu-id="5795c-123">Dodawanie MOVEit Transfer — integracji z usługą Azure AD z galerii</span><span class="sxs-lookup"><span data-stu-id="5795c-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
<span data-ttu-id="5795c-124">Aby skonfigurować integrację MOVEit Transfer — integracji usługi Azure AD do usługi Azure AD, należy dodać MOVEit Transfer — integracji usługi Azure AD z galerii z listą zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5795c-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5795c-125">**Aby dodać MOVEit Transfer — integracji z usługą Azure AD z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5795c-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5795c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5795c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="5795c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5795c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5795c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5795c-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="5795c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5795c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="5795c-133">W polu wyszukiwania wpisz **MOVEit Transfer — integracji z usługą Azure AD**, wybierz pozycję **MOVEit Transfer — integracji z usługą Azure AD** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikacja.</span><span class="sxs-lookup"><span data-stu-id="5795c-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span></span>

    ![MOVEit Transfer — integracji z usługą Azure AD na liście wyników](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5795c-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5795c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5795c-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MOVEit Transfer — integracji z usługą Azure AD w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5795c-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5795c-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w MOVEit Transfer — integracji z usługą Azure AD jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5795c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span></span> <span data-ttu-id="5795c-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w MOVEit Transfer — integracji z usługą Azure AD musi się.</span><span class="sxs-lookup"><span data-stu-id="5795c-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span></span>

<span data-ttu-id="5795c-139">W MOVEit Transfer — integracji z usługą Azure AD, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5795c-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5795c-140">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z MOVEit Transfer — integracji z usługą Azure AD, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5795c-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5795c-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5795c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5795c-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5795c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5795c-143">**[Tworzenie przeniesienia MOVEit - użytkownika testowego integracji usługi Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta MOVEit Transfer — integracji z usługą Azure AD połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5795c-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5795c-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5795c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5795c-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5795c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5795c-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5795c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5795c-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w transferu MOVEit - aplikacji integracji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5795c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="5795c-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z MOVEit Transfer — integracji z usługą Azure AD, należy wykonać następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5795c-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="5795c-149">W portalu Azure na **MOVEit Transfer — integracji z usługą Azure AD** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5795c-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="5795c-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5795c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="5795c-153">Na **MOVEit Transfer — adresy URL i integracji z usługą Azure AD domeny** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5795c-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="5795c-155">a.</span><span class="sxs-lookup"><span data-stu-id="5795c-155">a.</span></span> <span data-ttu-id="5795c-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="5795c-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="5795c-157">b.</span><span class="sxs-lookup"><span data-stu-id="5795c-157">b.</span></span> <span data-ttu-id="5795c-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="5795c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="5795c-159">c.</span><span class="sxs-lookup"><span data-stu-id="5795c-159">c.</span></span> <span data-ttu-id="5795c-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="5795c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="5795c-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5795c-161">These values are not real.</span></span> <span data-ttu-id="5795c-162">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5795c-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5795c-163">Może się odwoływać te wartości później w **adres URL metadanych dostawcy usługi** sekcji lub skontaktuj się z [MOVEit Transfer — zespołem pomocy technicznej klienta integracji usługi Azure AD](https://community.ipswitch.com/s/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="5795c-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span></span>

4. <span data-ttu-id="5795c-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5795c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="5795c-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5795c-166">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="5795c-168">Zaloguj się do dzierżawy MOVEit Transfer jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5795c-168">Sign on to your MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="5795c-169">W lewym okienku nawigacji, kliknij polecenie **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="5795c-169">On the left navigation pane, click **Settings**.</span></span>

    ![Strona aplikacji w sekcji Ustawienia](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="5795c-171">Kliknij przycisk **pojedynczego logować** łącza, która znajduje się w **zasad zabezpieczeń -> uwierzytelniania użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5795c-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Strony aplikacji na zasady zabezpieczeń](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="5795c-173">Kliknij łącze adres URL metadanych, aby pobrać dokumentu metadanych.</span><span class="sxs-lookup"><span data-stu-id="5795c-173">Click the Metadata URL link to download the metadata document.</span></span>

    ![Adres URL metadanych dostawcy usługi](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="5795c-175">Sprawdź **entityID** odpowiada **identyfikator** w **MOVEit Transfer — integracji z usługą Azure AD domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5795c-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="5795c-176">Sprawdź **AssertionConsumerService** odpowiada adresu URL lokalizacji **adres URL odpowiedzi** w **MOVEit Transfer — adresy URL i integracji z usługą Azure AD domeny** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5795c-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="5795c-178">Kliknij przycisk **Dodawanie dostawcy tożsamości** przycisk, aby dodać nowego dostawcę tożsamości federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="5795c-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>

    ![Dodaj dostawcę tożsamości](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="5795c-180">Kliknij przycisk **Przeglądaj...**  i wybierz plik metadanych, który został pobrany z portalu Azure, następnie kliknij przycisk **Dodawanie dostawcy tożsamości** można przekazać pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="5795c-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span></span>

    ![Dostawca tożsamości SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="5795c-182">Wybierz opcję "**tak**" jako **włączone** w **ustawień dostawcy tożsamości federacyjnych edycji...**  i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5795c-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Ustawienia dostawcy tożsamości federacyjnych](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="5795c-184">W **Edycja ustawień tożsamości federacyjnych dostawca użytkownika** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5795c-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span></span>
    
    ![Edytuj ustawienia dostawcy tożsamości federacyjnych](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="5795c-186">a.</span><span class="sxs-lookup"><span data-stu-id="5795c-186">a.</span></span> <span data-ttu-id="5795c-187">Wybierz **SAML NameID** jako **nazwa logowania**.</span><span class="sxs-lookup"><span data-stu-id="5795c-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="5795c-188">b.</span><span class="sxs-lookup"><span data-stu-id="5795c-188">b.</span></span> <span data-ttu-id="5795c-189">Wybierz **innych** jako **imię i nazwisko** i **nazwa atrybutu** pole tekstowe Podaj wartość: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="5795c-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="5795c-190">c.</span><span class="sxs-lookup"><span data-stu-id="5795c-190">c.</span></span> <span data-ttu-id="5795c-191">Wybierz **innych** jako **E-mail** i **nazwa atrybutu** pole tekstowe Podaj wartość: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="5795c-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="5795c-192">d.</span><span class="sxs-lookup"><span data-stu-id="5795c-192">d.</span></span> <span data-ttu-id="5795c-193">Wybierz **tak** jako **automatyczne tworzenie konta logowaniu**.</span><span class="sxs-lookup"><span data-stu-id="5795c-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="5795c-194">e.</span><span class="sxs-lookup"><span data-stu-id="5795c-194">e.</span></span> <span data-ttu-id="5795c-195">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5795c-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="5795c-196">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5795c-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5795c-197">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5795c-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5795c-198">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5795c-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5795c-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5795c-199">Create an Azure AD test user</span></span>

<span data-ttu-id="5795c-200">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5795c-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="5795c-202">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5795c-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5795c-203">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5795c-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5795c-205">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5795c-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5795c-207">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="5795c-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5795c-209">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5795c-209">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5795c-211">a.</span><span class="sxs-lookup"><span data-stu-id="5795c-211">a.</span></span> <span data-ttu-id="5795c-212">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5795c-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5795c-213">b.</span><span class="sxs-lookup"><span data-stu-id="5795c-213">b.</span></span> <span data-ttu-id="5795c-214">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5795c-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5795c-215">c.</span><span class="sxs-lookup"><span data-stu-id="5795c-215">c.</span></span> <span data-ttu-id="5795c-216">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="5795c-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5795c-217">d.</span><span class="sxs-lookup"><span data-stu-id="5795c-217">d.</span></span> <span data-ttu-id="5795c-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5795c-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="5795c-219">Tworzenie przeniesienia MOVEit - użytkownika testowego integracji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5795c-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="5795c-220">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w MOVEit Transfer — integracji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5795c-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="5795c-221">MOVEit Transfer — integracji z usługą Azure AD obsługę just in time, które zostało włączone.</span><span class="sxs-lookup"><span data-stu-id="5795c-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="5795c-222">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="5795c-222">There is no action item for you in this section.</span></span> <span data-ttu-id="5795c-223">Nowy użytkownik został utworzony podczas próby dostępu MOVEit Transfer — integracji usługi Azure AD, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="5795c-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="5795c-224">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [MOVEit Transfer — zespołem pomocy technicznej klienta integracji usługi Azure AD](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="5795c-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5795c-225">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5795c-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="5795c-226">W tej sekcji musisz włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do transferu MOVEit - integracji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5795c-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="5795c-228">**Aby przypisać Simona Britta MOVEit Transfer — integracji z usługą Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5795c-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="5795c-229">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5795c-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5795c-231">Na liście aplikacji zaznacz **MOVEit Transfer — integracji z usługą Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="5795c-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![MOVEit Transfer — integracji z usługą Azure AD łącza na liście aplikacji](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="5795c-233">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5795c-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="5795c-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5795c-235">Click **Add** button.</span></span> <span data-ttu-id="5795c-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5795c-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="5795c-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5795c-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5795c-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5795c-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5795c-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5795c-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5795c-241">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5795c-241">Test single sign-on</span></span>

<span data-ttu-id="5795c-242">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5795c-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5795c-243">Po kliknięciu MOVEit Transfer — integracji z usługą Azure AD kafelka w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do transferu MOVEit - aplikacji integracji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5795c-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5795c-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5795c-244">Additional resources</span></span>

* [<span data-ttu-id="5795c-245">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5795c-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5795c-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5795c-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

