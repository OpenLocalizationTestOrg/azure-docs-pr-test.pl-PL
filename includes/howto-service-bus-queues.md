## <a name="what-are-service-bus-queues"></a>Czym są kolejki usługi Service Bus?
Kolejki usługi Service Bus obsługują model komunikacji z użyciem **komunikatów obsługiwanych przez blokera**. Podczas korzystania z kolejek składniki aplikacji rozproszonej nie komunikują się bezpośrednio ze sobą, lecz wymieniają komunikaty za pośrednictwem kolejki, która działa jako pośrednik (broker). Producent komunikatu (nadawca) przekazuje komunikat toohello kolejki i kontynuuje jego przetwarzanie. Konsument komunikatu (odbiorca) asynchronicznie, pobiera hello wiadomości z kolejki hello i przetwarza je. producent Hello nie ma toowait na odpowiedź od konsumenta hello w kolejności toocontinue tooprocess i wysyłanie dalszych komunikatów. Kolejki oferują **pierwszy na wejściu — pierwszy na wyjściu (FIFO)** komunikatu tooone dostarczania lub więcej konkurujących konsumentów. Oznacza to, że komunikaty są zwykle odbierane i przetwarzane przez hello odbiorców w kolejności hello, w którym zostały one dodane toohello kolejki, a każdy komunikat jest odbierany i przetwarzany przez tylko jednego odbiorcę komunikatów.

![QueueConcepts](./media/howto-service-bus-queues/sb-queues-08.png)

Kolejki usługi Service Bus to technologia ogólnego przeznaczenia, która może być używana w wielu różnych scenariuszach:

* Komunikacja między rolami sieci Web i procesów roboczych w wielowarstwowej aplikacji Azure.
* Komunikacja między aplikacjami lokalnymi i hostowanymi na platformie Azure w rozwiązaniu hybrydowym.
* Komunikacja między składnikami aplikacji rozproszonej działającej lokalnie w różnych organizacjach lub działach organizacji.

Korzystanie z kolejek umożliwia tooscale można łatwiej aplikacji, a następnie włącz więcej architektura tooyour odporności.


