# gas-meter-for-homeassistant
<b>gas meter for homeassistant</b>

#code in "gas-meter-for-homeassistant.yaml" bazuje na: https://github.com/klaasnicolaas/home-assistant-glow/blob/main/home_assistant_glow.yaml

Pomysł odczytu wskazań gazomierza narodził się w wyniku innego projektu: https://github.com/klaasnicolaas/home-assistant-glow
Realizując odczyt modyfikowałem kod dostępny w ww. repozytorium.

Poniżej postaram się opisać sposób w jaki realizuję odczyt gazomierza. W moim przypadku jest to gazomierz Apator Metrix UG G4.

Do gazomierza został podłączony, tzw. Nadajnik impulsów NI-3 dedykowany do ww. W skrócie jest to kontaktron w odpowiedniej obudowie, pasujący do gniazda gazomierza.

W Polsce możliwość podłączenia należy uzgodnić z Polską Spółką Gazowniczą, operatorem infrastruktury gazowej. (kontakt dla woj. mazowieckiego: pomiary.warszawa@psgaz.pl, Polska Spółka Gazownictwa sp. z o.o. Oddział Zakład Gazowniczy w Warszawie, tel. 22 667 34 66, fax. 22 667 34 80, adres korespondencyjny: ul. Równoległa 4a, 02-235 Warszawa). Spółka wyraziła zgodę na odczyt impulsów pod warunkiem zastosowania tzw. Bariery iskroodpornej. Ja zakupiłem w popularnym serwisie aukcyjnym barierę galwaniczną firmy EATON, model: „MTL7787-”.

Pierwszym problemem jaki napotkałem w realizacji licznika impulsów była właśnie ww. bariera, która wprowadza dodatkową rezystancję w obwodzie z kontaktronem. Powoduje to, że po zwarciu mamy „słabą” masę. Impuls ten był niewystarczający dla popularnych układów ESP8266 czy ESP32. W celu jego rozwiązania zastosowałem swojego rodzaju „wzmacniacz”, który powstał poprzez wylutowanie diody światłoczułej z układu LM393. Na jego wyjściu D0 mamy już mocny sygnał.

Drugim problemem był zbyt długi czas zwarcia kontaktrona, np. gdy licznik zatrzymywał się w pozycji „0” na ostatniej tarczy. Zamknięcie takie może trwać godzinami, aż gaz znów zacznie być pobierany. W celu rozwiązania tej sytuacji zastosowałem widoczny na schemacie moduł czasowy CE030 z ustawionym programem 12. Czasy T1 oraz T2 ustawiłem na 200 ms.

Następnie wystarczyło pin NO układu CE030 podłączyć, np. z pinem D4 w WEMOS D1 mini. W pliku .yaml dostępny jest kod dla ESPHome.
 Kod dla ESPHome jest dostępny w pliku .yaml.

Powodzenia w realizacji.

Pozdrawiam 

Schemat:
<p align="center">
  <img width="80%" src="scheme.png">
</p>
