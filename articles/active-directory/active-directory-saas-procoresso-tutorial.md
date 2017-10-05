---
title: "Samouczek: Integracji usługi Azure Active Directory z logowania jednokrotnego Procore | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Procore logowania jednokrotnego."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 042a41eaa6bb21670b4c12068f1b017222f64b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="2fefe-103">Samouczek: Integracji Azure Active Directory z Procore logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="2fefe-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="2fefe-104">Z tego samouczka dowiesz się integrowanie Procore logowania jednokrotnego w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2fefe-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2fefe-105">Integrowanie Procore rejestracji Jednokrotnej z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2fefe-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2fefe-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Procore logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="2fefe-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="2fefe-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Procore SSO (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fefe-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2fefe-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="2fefe-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2fefe-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2fefe-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="2fefe-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2fefe-110">Prerequisites</span></span>

<span data-ttu-id="2fefe-111">Aby skonfigurować integrację usługi Azure AD z Procore logowania jednokrotnego, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2fefe-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="2fefe-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fefe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2fefe-113">Procore logowania jednokrotnego jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2fefe-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2fefe-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2fefe-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2fefe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2fefe-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2fefe-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2fefe-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2fefe-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2fefe-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2fefe-118">Scenario description</span></span>
<span data-ttu-id="2fefe-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2fefe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2fefe-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2fefe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2fefe-121">Dodawanie Procore rejestracji Jednokrotnej z galerii</span><span class="sxs-lookup"><span data-stu-id="2fefe-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="2fefe-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2fefe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="2fefe-123">Dodawanie Procore rejestracji Jednokrotnej z galerii</span><span class="sxs-lookup"><span data-stu-id="2fefe-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="2fefe-124">Aby skonfigurować integrację Procore logowania jednokrotnego do usługi Azure AD, należy dodać Procore rejestracji Jednokrotnej z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2fefe-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2fefe-125">**Aby dodać Procore rejestracji Jednokrotnej z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2fefe-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2fefe-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2fefe-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="2fefe-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2fefe-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="2fefe-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="2fefe-133">W polu wyszukiwania wpisz **Procore logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-133">In the search box, type **Procore SSO**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="2fefe-135">W panelu wyników wybierz **Procore logowania jednokrotnego**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="2fefe-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2fefe-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2fefe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2fefe-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej Procore logowaniem jednokrotnym w oparciu o użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="2fefe-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2fefe-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w Procore rejestracji Jednokrotnej dla użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2fefe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="2fefe-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Procore logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="2fefe-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Procore logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="2fefe-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Procore logowania jednokrotnego, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="2fefe-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2fefe-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2fefe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2fefe-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2fefe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2fefe-145">**[Tworzenie użytkownika testowego Procore logowania jednokrotnego](#creating-a-procore-sso-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Procore Usługa rejestracji Jednokrotnej jest połączona z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2fefe-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2fefe-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2fefe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2fefe-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="2fefe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2fefe-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2fefe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2fefe-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji Procore logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="2fefe-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Procore logowania jednokrotnego, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2fefe-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="2fefe-151">W portalu zarządzania Azure na **Procore logowania jednokrotnego** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="2fefe-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="2fefe-155">Na **Procore domena logowania jednokrotnego i adresy URL** sekcji, użytkownik nie trzeba wykonywać żadnych czynności, jak aplikacja już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="2fefe-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="2fefe-157">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2fefe-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="2fefe-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2fefe-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2fefe-161">Na **Procore konfiguracji logowania jednokrotnego** kliknij **Konfigurowanie logowania jednokrotnego Procore** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="2fefe-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2fefe-162">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="2fefe-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="2fefe-164">Aby skonfigurować logowanie jednokrotne w **Procore logowania jednokrotnego** strona, zaloguj się do witryny procore firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2fefe-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="2fefe-165">Z listy przybornika w dół, kliknij pozycję **Admin** aby otworzyć stronę ustawienia logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="2fefe-167">Wklej wartości w polach, zgodnie z opisem poniżej-</span><span class="sxs-lookup"><span data-stu-id="2fefe-167">Paste the values in the boxes as described below-</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="2fefe-169">a.</span><span class="sxs-lookup"><span data-stu-id="2fefe-169">a.</span></span> <span data-ttu-id="2fefe-170">W **pojedynczy znak na adres URL wystawcy** okno, wklej identyfikator jednostki SAML skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2fefe-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="2fefe-171">b.</span><span class="sxs-lookup"><span data-stu-id="2fefe-171">b.</span></span> <span data-ttu-id="2fefe-172">W **SAML logowania na docelowy adres URL** okno, Wklej SAML pojedynczy znak na adres URL usługi skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2fefe-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="2fefe-173">c.</span><span class="sxs-lookup"><span data-stu-id="2fefe-173">c.</span></span> <span data-ttu-id="2fefe-174">Teraz otworzyć **XML metadanych** pobrane wcześniej z portalu Azure i skopiuj certyfikat w tagu o nazwie **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="2fefe-175">Wklej skopiowane wartości do **certyfikatu rejestracji jednokrotnej x509** pole.</span><span class="sxs-lookup"><span data-stu-id="2fefe-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="2fefe-176">Polecenie **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="2fefe-177">Po tych ustawień, użytkownik musi wysłać **nazwy domeny** (np. **contoso.com**) za pomocą którego logujesz się do Procore do [zespołem pomocy technicznej Procore](https://support.procore.com/) i zostaną one Aktywuj federacyjną rejestracją Jednokrotną dla tej domeny.</span><span class="sxs-lookup"><span data-stu-id="2fefe-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2fefe-178">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fefe-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="2fefe-179">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2fefe-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="2fefe-181">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2fefe-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2fefe-182">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2fefe-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2fefe-184">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="2fefe-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2fefe-186">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2fefe-188">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2fefe-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2fefe-190">a.</span><span class="sxs-lookup"><span data-stu-id="2fefe-190">a.</span></span> <span data-ttu-id="2fefe-191">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2fefe-192">b.</span><span class="sxs-lookup"><span data-stu-id="2fefe-192">b.</span></span> <span data-ttu-id="2fefe-193">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2fefe-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2fefe-194">c.</span><span class="sxs-lookup"><span data-stu-id="2fefe-194">c.</span></span> <span data-ttu-id="2fefe-195">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2fefe-196">d.</span><span class="sxs-lookup"><span data-stu-id="2fefe-196">d.</span></span> <span data-ttu-id="2fefe-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="2fefe-198">Tworzenie użytkownika testowego Procore logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="2fefe-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="2fefe-199">Wykonaj następujące czynności, aby utworzyć użytkownika testowego Procore w bok.</span><span class="sxs-lookup"><span data-stu-id="2fefe-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="2fefe-200">Zaloguj się do witryny procore firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2fefe-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="2fefe-201">Z listy przybornika w dół, kliknij pozycję **katalogu** aby otworzyć stronę katalogu firmy.</span><span class="sxs-lookup"><span data-stu-id="2fefe-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="2fefe-203">Polecenie **dodać osobę** opcję, aby otworzyć formularz i wprowadzić wykonania następujących opcji -</span><span class="sxs-lookup"><span data-stu-id="2fefe-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="2fefe-205">a.</span><span class="sxs-lookup"><span data-stu-id="2fefe-205">a.</span></span> <span data-ttu-id="2fefe-206">W **imię** pole tekstowe, imię użytkownika typu, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="2fefe-207">b.</span><span class="sxs-lookup"><span data-stu-id="2fefe-207">b.</span></span> <span data-ttu-id="2fefe-208">W **nazwisko** pole tekstowe, nazwisko użytkownika typu, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="2fefe-209">c.</span><span class="sxs-lookup"><span data-stu-id="2fefe-209">c.</span></span> <span data-ttu-id="2fefe-210">W **adres E-mail** , adres e-mail użytkownika typu pole tekstowe, takich jak  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="2fefe-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="2fefe-211">d.</span><span class="sxs-lookup"><span data-stu-id="2fefe-211">d.</span></span> <span data-ttu-id="2fefe-212">Wybierz **szablon uprawnień** jako **później Zastosuj szablon uprawnień**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="2fefe-213">e.</span><span class="sxs-lookup"><span data-stu-id="2fefe-213">e.</span></span> <span data-ttu-id="2fefe-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-214">Click **Create**.</span></span>

4. <span data-ttu-id="2fefe-215">Sprawdź i zaktualizuj szczegóły dla nowo dodanego kontaktu.</span><span class="sxs-lookup"><span data-stu-id="2fefe-215">Check and update the details for the newly added contact.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="2fefe-217">Polecenie **zapisywanie i wysyłanie Invitiation** (Jeśli wymagane jest zaproszenia pocztą) lub **zapisać** (Zapisz bezpośrednio) do ukończenia rejestracji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2fefe-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2fefe-219">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fefe-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2fefe-220">W tej sekcji można włączyć Simona Britta do udostępnienia jej Procore logowania jednokrotnego za pomocą platformy Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2fefe-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="2fefe-222">**Aby przypisać Simona Britta Procore logowania jednokrotnego, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2fefe-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="2fefe-223">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2fefe-225">Na liście aplikacji zaznacz **Procore logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-225">In the applications list, select **Procore SSO**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="2fefe-227">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2fefe-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="2fefe-229">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2fefe-229">Click **Add** button.</span></span> <span data-ttu-id="2fefe-230">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="2fefe-232">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="2fefe-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2fefe-233">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2fefe-234">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2fefe-235">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2fefe-235">Testing single sign-on</span></span>

<span data-ttu-id="2fefe-236">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2fefe-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2fefe-237">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="2fefe-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="2fefe-238">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="2fefe-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="2fefe-239">Po kliknięciu kafelka Procore logowania jednokrotnego w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Procore logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2fefe-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2fefe-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2fefe-240">Additional resources</span></span>

* [<span data-ttu-id="2fefe-241">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2fefe-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2fefe-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2fefe-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

