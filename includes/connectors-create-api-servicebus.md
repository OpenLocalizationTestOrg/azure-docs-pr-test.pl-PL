### <a name="prerequisites"></a>Wymagania wstępne
Musi mieć [usługi Service Bus](https://azure.microsoft.com/services/service-bus/) konta.  

Zanim użyjesz swojego konta usługi Azure Service Bus w aplikacji logiki, należy uwierzytelnić konta magistrali usługi tooyour tooconnect hello logiki aplikacji. Na szczęście można w tym z aplikacji logiki na powitania portalu Azure.  

Oto hello kroki tooauthorize Twojego tooyour tooconnect aplikacji logiki konta usługi Service Bus:  

1. Wybierz tooService połączenia magistrali, w Projektancie aplikacji logiki hello, toocreate **Pokaż Microsoft zarządzanych interfejsów API** na liście rozwijanej hello. Następnie wprowadź **usługi magistrali** hello pola wyszukiwania. Wybierz wyzwalacz hello lub akcja ma toouse.  
    ![Obraz połączenia usługi Service Bus 1](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. Jeśli nie utworzono żadnych tooService połączenia magistrali przed, będzie tooprovide zostanie wyświetlony monit o poświadczenia magistrali usług. Te poświadczenia są używane tooauthorize Twojego tooand tooconnect aplikacji logiki dostęp do danych konta usługi Service Bus. Łącznik usługi Service Bus Hello musi hello parametry połączenia dla przestrzeni nazw usługi Service Bus hello. Wymagany jest również **Zarządzaj** uprawnienia. Tooknow dobrze, jeśli parametry połączenia dla przestrzeni nazw hello lub określonej jednostki czy zawiera on hello `EntityPath` parametru. Jeśli tak, nie jest hello ciąg połączenia na odpowiednie dla aplikacji logiki.  
    ![Parametry połączenia magistrali usług](./media/connectors-create-api-servicebus/connectionstring.png)
3. Po otrzymaniu hello parametry połączenia dla przestrzeni nazw hello umożliwia dla hello połączenia interfejsu API w aplikacjach logiki.  
    ![Obraz połączenia usługi Service Bus 2](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. Utworzono połączenie hello powiadomienia i są teraz wolnego tooproceed z hello innych czynności w aplikacji logiki.  
    ![Obraz połączenia usługi Service Bus 3](./media/connectors-create-api-servicebus/servicebus-3.png)   

