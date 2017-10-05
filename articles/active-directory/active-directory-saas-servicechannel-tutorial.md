---
title: 'Samouczek: Integracji Azure Active Directory z obiektu ServiceChannel | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i obiektu ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 7e1dad18ff0ae9a9102b789b2cb32e7b96ed3d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="ed0c0-103">Samouczek: Integracji Azure Active Directory z obiektu ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="ed0c0-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="ed0c0-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) obiektu ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed0c0-105">Integrowanie kanale usługi z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ed0c0-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ed0c0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do obiektu ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="ed0c0-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="ed0c0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do obiektu ServiceChannel (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed0c0-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed0c0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="ed0c0-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="ed0c0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed0c0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed0c0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ed0c0-110">Prerequisites</span></span>

<span data-ttu-id="ed0c0-111">Aby skonfigurować integrację usługi Azure AD z obiektu ServiceChannel, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ed0c0-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="ed0c0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed0c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed0c0-113">Obiektu ServiceChannel jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ed0c0-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed0c0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed0c0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ed0c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed0c0-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ed0c0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed0c0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed0c0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ed0c0-118">Scenario description</span></span>
<span data-ttu-id="ed0c0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed0c0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ed0c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed0c0-121">Dodawanie obiektu ServiceChannel z galerii</span><span class="sxs-lookup"><span data-stu-id="ed0c0-121">Adding ServiceChannel from the gallery</span></span>
2. <span data-ttu-id="ed0c0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ed0c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="ed0c0-123">Dodawanie obiektu ServiceChannel z galerii</span><span class="sxs-lookup"><span data-stu-id="ed0c0-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="ed0c0-124">Aby skonfigurować integrację usługi Azure AD obiektu ServiceChannel, należy dodać obiektu ServiceChannel z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ed0c0-125">**Aby dodać obiektu ServiceChannel z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ed0c0-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ed0c0-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ed0c0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ed0c0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ed0c0-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ed0c0-133">W polu wyszukiwania wpisz **obiektu ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-133">In the search box, type **ServiceChannel**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="ed0c0-135">W panelu wyników wybierz **obiektu ServiceChannel**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ed0c0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ed0c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ed0c0-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z obiektu ServiceChannel w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ed0c0-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w kanale usługi jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="ed0c0-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w kanale usługi.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="ed0c0-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w kanale usługi.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="ed0c0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z obiektu ServiceChannel, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ed0c0-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ed0c0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ed0c0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed0c0-145">**[Tworzenie użytkownika testowego obiektu ServiceChannel](#creating-a-servicechannel-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="ed0c0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed0c0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ed0c0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ed0c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ed0c0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji obiektu ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="ed0c0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z obiektu ServiceChannel, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ed0c0-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="ed0c0-151">W portalu zarządzania Azure na **obiektu ServiceChannel** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ed0c0-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="ed0c0-155">Na **adresy URL i domeny obiektu ServiceChannel** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ed0c0-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="ed0c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-157">a.</span></span> <span data-ttu-id="ed0c0-158">W **identyfikator** tekstowym, wpisz wartość, jak:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="ed0c0-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="ed0c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-159">b.</span></span> <span data-ttu-id="ed0c0-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="ed0c0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed0c0-161">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-161">Please note that these are not the real values.</span></span> <span data-ttu-id="ed0c0-162">Należy zaktualizować te wartości z rzeczywistego identyfikatora i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ed0c0-163">W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="ed0c0-164">Skontaktuj się z [zespołem pomocy technicznej obiektu ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

4. <span data-ttu-id="ed0c0-165">Aplikacja obiektu ServiceChannel oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ed0c0-166">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="ed0c0-167">**NameIdentifier (identyfikator użytkownika)** jest tylko obowiązkowe oświadczeń, a wartość domyślna to **user.userprincipalname** , ale oczekuje obiektu ServiceChannel, aby być mapowane z **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="ed0c0-168">Jeśli planujesz włączyć tylko w czasie Inicjowanie obsługi użytkowników, następnie należy dodać następujące oświadczeń w sposób przedstawiony poniżej.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="ed0c0-169">**Rola** oświadczeń musi być zamapowany na **user.assignedroles** zawierającą roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="ed0c0-170">Może się odwoływać przewodnik obiektu ServiceChannel [tutaj](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) więcej wskazówki dotyczące oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="ed0c0-172">Kliknij [tutaj](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) wiedzieć, jak skonfigurować **roli** w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed0c0-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) to know how to configure **Role** in Azure AD</span></span>

5. <span data-ttu-id="ed0c0-173">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustawić atrybutów.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="ed0c0-174">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="ed0c0-174">Attribute Name</span></span> | <span data-ttu-id="ed0c0-175">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="ed0c0-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="ed0c0-176">Rola</span><span class="sxs-lookup"><span data-stu-id="ed0c0-176">Role</span></span>| <span data-ttu-id="ed0c0-177">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="ed0c0-177">user.assignedroles</span></span> |

    <span data-ttu-id="ed0c0-178">a.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-178">a.</span></span> <span data-ttu-id="ed0c0-179">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="ed0c0-182">b.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-182">b.</span></span> <span data-ttu-id="ed0c0-183">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ed0c0-184">c.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-184">c.</span></span> <span data-ttu-id="ed0c0-185">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ed0c0-186">d.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-186">d.</span></span> <span data-ttu-id="ed0c0-187">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="ed0c0-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="ed0c0-188">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="ed0c0-190">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-190">Click **Save**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ed0c0-192">Na **konfiguracji obiektu ServiceChannel** , kliknij przycisk **skonfigurować obiektu ServiceChannel** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ed0c0-193">Należy pamiętać, **identyfikator jednostka SAML** z **krótkimi opisami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

9. <span data-ttu-id="ed0c0-194">Skonfigurować logowanie jednokrotne w **obiektu ServiceChannel** stronie, musisz wysłać pobrany **certyfikatu (Base64)** i **identyfikator jednostki SAML** do [obiektu ServiceChannel obsługuje zespołu](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="ed0c0-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="ed0c0-195">One będzie skonfigurowanie tego numeru w celu połączenia logowania jednokrotnego SAML prawidłowo po obu stronach.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ed0c0-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed0c0-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="ed0c0-197">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ed0c0-199">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ed0c0-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ed0c0-200">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ed0c0-202">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ed0c0-204">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed0c0-206">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ed0c0-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed0c0-208">a.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-208">a.</span></span> <span data-ttu-id="ed0c0-209">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed0c0-210">b.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-210">b.</span></span> <span data-ttu-id="ed0c0-211">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ed0c0-212">c.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-212">c.</span></span> <span data-ttu-id="ed0c0-213">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ed0c0-214">d.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-214">d.</span></span> <span data-ttu-id="ed0c0-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="ed0c0-216">Tworzenie użytkownika testowego obiektu ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="ed0c0-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="ed0c0-217">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="ed0c0-218">Aby Inicjowanie obsługi użytkowników pełne, skontaktuj się z [obiektu ServiceChannel zespołem pomocy technicznej](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="ed0c0-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ed0c0-219">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed0c0-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ed0c0-220">W tej sekcji można włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udostępnienie jej do obiektu ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ed0c0-222">**Aby przypisać Simona Britta obiektu ServiceChannel, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ed0c0-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="ed0c0-223">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ed0c0-225">Na liście aplikacji zaznacz **obiektu ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-225">In the applications list, select **ServiceChannel**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="ed0c0-227">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ed0c0-229">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-229">Click **Add** button.</span></span> <span data-ttu-id="ed0c0-230">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ed0c0-232">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ed0c0-233">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed0c0-234">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ed0c0-235">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ed0c0-235">Testing single sign-on</span></span>

<span data-ttu-id="ed0c0-236">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ed0c0-237">Po kliknięciu kafelka obiektu ServiceChannel w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji obiektu ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="ed0c0-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed0c0-238">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ed0c0-238">Additional resources</span></span>

* [<span data-ttu-id="ed0c0-239">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed0c0-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed0c0-240">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ed0c0-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png