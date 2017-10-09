### <a name="prerequisites"></a>Wymagania wstępne
* Konta usługi Twilio
* Zweryfikowano numer telefonu usługi Twilio, który może odbierać programu SMS
* Zweryfikowano numer telefonu usługi Twilio, która umożliwia wysyłanie SMS

> [!NOTE]
> Jeśli używasz konta próbnego usługi Twilio, można wysłać tylko SMS zbyt**zweryfikować** numerów telefonów.  
> 
> 

Aby korzystać z konta usługi Twilio, w aplikacji logiki, musisz autoryzować hello logiki aplikacji tooconnect tooyour usługi Twilio konta. Na szczęście można w tym z aplikacji logiki na powitania portalu Azure. 

Oto hello kroki tooauthorize Twojego tooyour tooconnect aplikacji logiki konta usługi Twilio:

1. Wybierz tooTwilio połączenia, w Projektancie aplikacji logiki hello, toocreate **Pokaż Microsoft zarządzanych interfejsów API** w hello listy rozwijanej, a następnie wprowadź *usługi Twilio* w polu wyszukiwania hello. Wybierz wyzwalacz hello lub Ci się spodoba toouse akcji:  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. Jeśli nie utworzono żadnych tooTwilio połączenia przed, zostanie wyświetlony zostanie wyświetlony monit o tooprovide poświadczeń usługi Twilio. Te poświadczenia można używane tooauthorize Twojego tooconnect aplikacji logiki do i uzyskać dostęp do konta usługi Twilio danych:  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. Będziesz potrzebować hello **identyfikator konta usługi Twilio** i **token dostępu usługi Twilio** z pulpitu nawigacyjnego hello w usługi Twilio, więc zalogować toograb teraz konta usługi Twilio tooyour te dwa rodzaje informacji:  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. Usługi Twilio i logiki aplikacji użyj różnych nazw tooidentify te dwa rodzaje informacji. Oto, jak należy mapować je toohello logiki aplikacji w oknie dialogowym:![](./media/connectors-create-api-twilio/twilio-3.png)  
5. Wybierz hello **utworzyć połączenie** przycisk:  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. Zwróć uwagę, hello połączenie zostało utworzone i są teraz wolnego tooproceed z hello innych czynności w aplikacji logiki:  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

