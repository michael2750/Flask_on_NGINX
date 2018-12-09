## Flask applikation kørende på NGINX
Gruppe E1: Laura Hartig, Nicolai Mikkelsen & Michael Daugbjerg.

*Hvis du gør brug af Flask i en større applikation, er der stor sandsynlighed for dette ikke er den bedste løsning. Flask har nemlig sine begrænsninger, når det kommer til at håndtere requests, og dette kan blive et problem, især for store virksomheder. Hvis antallet af requests overstiger den mængde, som Flask er i stand til at håndtere, kan det nemlig skabe en bottleneck i applikationen. En nem løsning for at undgå dette, ville være at implementere NGINX. Ved at bruge NGINX ville virksomheder  kunne øge applikations stabilitet markant og samtidig undgå langsom response time.*


#### Hvem bruger Flask?
[Flask](http://flask.pocoo.org/docs/1.0/) er blevet meget mere populært inden for softwareudvikling siden udgivelsen i 2010, men dens funktion til at skalere i forhold til requests per second(RPS) er i den lave ende i forhold til andre værktøjer, som er tilgængelige.
Flask er open source og let at implementere, hvilket gør det attraktivt til hurtigt at lave en applikation. Flask bliver typisk brugt af dem, som skal sætte en simpel web applikation op med en form for routing, uden at skulle implementere et tykt interface. Samtidig kan Flask være en god learning experience, da det kun indeholder ‘bare minimum’ i sig, og derfor giver en større udfordring for udvikleren som øger erfaring inden for programmering.


#### Hvad er Flask i stand til?
Flask er et micro-framework, hvilket betyder at det ikke kommer med en masse fyld i form af moduler og features. Flask lader extentions om at håndtere disse features, så man nemmere kan tilpasse applikationen og på den måde kan udvikleren selv vælge, hvordan den skal opbygges. Dette gør Flask super brugervenligt, da extensions er meget nemme at implementere.

#### Hvilke ulemper har Flask?
[Mark Hildreth](https://stackoverflow.com/questions/20843486/what-are-the-limitations-of-the-flask-built-in-web-server?answertab=votes#tab-top) kommer ind på et af de svage punkter, som kommer med Flask. Frameworket er som udgangspunkt single threaded, altså vil Flask kun kunne håndtere et request ad gangen. Hvis et request rammer en bottleneck i applikationen, som tager f.eks 3 sekunder om at få et response, vil applikationen være sat i stå i mellemtiden. Flask kan køre multithreading, men det er stadig ikke tilstrækkeligt under ‘heavy load’, hvilket en større applikation typisk vil få.

![Flask_RPS](/images/Flask_RPS.png)

[Source](https://medium.com/@tschundeee/express-vs-flask-vs-go-acc0879c2122)


#### Hvad er løsningen til dette problem? 
Det gode ved Flask er, at det skalere godt i forhold til kode. Så hvis vi ser bort fra frameworkets RPS og får en anden service til at håndtere dem, kan man på den måde forhindre denne bottleneck i applikationen. Her er [NGINX](https://www.nginx.com/blog/testing-the-performance-of-nginx-and-nginx-plus-web-servers/) et passende værktøj, da det især er godt til at håndtere mange flere RPS.

#### Hvad er fordelen ved NGINX?
NGINX kan fungere som en webserver, reverse proxy & som en load balancer til flere servere eller services. Ved at bruge NGINX som en reverse proxy til Flask, kan man løse problemet med Flasks RPS. Her fungerer NGINX som en buffer, der håndtere requests for Flask applikationen og på den måde giver mere plads til at bearbejde requests og mindre ventetid. NGINX kan også håndtere mange concurrent connections, og sørger for at den belastning, som ligger på applikationen, ikke kun handler om at have god hardware. Så hvis man vil køre en applikation med Flask i threaded tilstand, handler det om, hvor mange kerner man har, og hvor hurtigt de kan processere instruktioner. Derfor vil man blive nødt til at anskaffe større og bedre hardware før Flask kan håndtere flere requests hvorimod NGINX er den softwaremæssige løsning på dette problem.

![NGINX_reverse_proxy](/images/NGINX_RP.png)

[Source](https://www.nginx.com/blog/maximizing-python-performance-with-nginx-parti-web-serving-and-caching/) 

#### Hvornår vil man bruge NGINX?
Flask ville fint kunne køre en mindre applikation, men NGINX ville være essentiel, hvis man overstiger det antal RPS som Flask kan håndtere. NGINX ville kunne frigøre Flask i at skulle håndtere [SSL](https://www.fairssl.dk/da/ssl-information/what-is-an-ssl-certificate, som er den del, der sørger for en sikker forbindelse i et HTTP request. Dette gør at Flask frit kan håndtere requestet uden at skulle lave et sikkerhedstjek. Billedet nedenfor repræsenterer NGINX RPS under forskellige omstændigheder. Skemaet er en oversigt over antallet af RPS ved `x` antal kerner og `n` KB størrelse på det data, som bliver sendt med requestet.

![NGINX_request_per_second](/images/NGINX_RPS.png)

[Source](https://www.nginx.com/blog/testing-the-performance-of-nginx-and-nginx-plus-web-servers/)

#### Hvad medfører denne løsning?
Ved at tilføje NGINX, vil det være en økonomisk besparelse i forhold til, hvis man ellers skulle ud og opgradere sit hardware, som alligevel på et tidspunkt ikke ville være tilstrækkeligt. Derudover skaber det også en hurtigere response time og derfor giver en mere tilfreds oplevelse ved brug af applikationen.

#### Konklusion
Vi valgte at bruge NGINX, da vores applikation skulle køres op imod en simulator. Her kunne man med det samme se på det antal RPS som ville blive sendt, at Flask umuligt ville kunne håndtere dette alene. Derfor valgte vi at bruge NGINX som en reverse proxy oven på vores Flask applikation, som gjorde det muligt, at kunne håndtere langt flere RPS som dermed opfyldte kravene til simulatoren.


[<-- Ressourcer](sources.md)

[<-- Billeder](/images)
