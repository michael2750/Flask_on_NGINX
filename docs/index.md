## Flask applikation kørende på NGINX
Hvis du gør brug af Flask i en større applikation, er der stor sandsynlighed for dette ikke er den bedste løsning, da Flask har sine begrænsninger i forhold til, at håndtere requests.
Flask kan blive et problem for virksomheder, hvis mængden af requests overstiger den mængde Flask er i stand til at håndtere, og dermed skaber en bottleneck i applikationen. En nem løsning ville være at implementere NGINX, så man derved kan undgå den bottleneck, der er opstået.
Ved at implementere NGINX vil firmaet både spare problemer angående klager, pga. et langsomt response, men den vil samtidig også øge applikationens stabilitet.

#### Hvem bruger Flask?
[Flask](http://flask.pocoo.org/docs/1.0/) er blevet meget mere populært inden for softwareudvikling siden udgivelsen i 2010, men dens funktion til at skalere i forhold til requests per second(RPS) er i den lave ende af de andre værktøjer, som er tilgængelige.
Flask er open source og let at implementere, hvilket gør det attraktivt til hurtigt at lave en applikation. Flask bliver typisk brugt af dem, som skal sætte en simpel web applikation op med en form for routing, uden at skulle implementere et tykt interface. Samtidig kan Flask være en god learning experience, da det kun indeholder ‘bare minimum’ i sig, og derfor giver en større udfordring for udvikleren som øger erfaring inden for programmering.

#### Hvad er Flask i stand til?
Da Flask er et micro-framework, betyder det at det ikke kommer med en masse fylde i form af moduler og features. Flask lader extentions om at håndtere disse features, så man nemmere kan tilpasse applikationen og derved kan udvikleren selv vælge hvordan den skal opbygges. Samtidig er Flask meget brugervenligt og kan nemt implementere disse extensions.

#### Hvilke ulemper har Flask?
[Mark Hildreth](https://stackoverflow.com/questions/20843486/what-are-the-limitations-of-the-flask-built-in-web-server?answertab=votes#tab-top) kommer ind på et af de svage punkter, som kommer med Flask. Frameworket er som udgangspunkt single threaded, altså vil Flask kun kunne håndtere et request ad gangen. Hvis et request rammer en bottleneck i applikationen, som tager f.eks 3 sekunder for at få et response, vil applikationen være sat i stå i mellemtiden. Flask kan køre multithreading, men det er stadig ikke tilstrækkeligt under ‘heavy load’, hvilket en større applikation typisk vil få.

![Flask](/images/Flask_RPS.png)

[Source](https://medium.com/@tschundeee/express-vs-flask-vs-go-acc0879c2122)


#### Hvad er løsningen til dette problem? 
Det gode ved Flask er at det skalere godt i forhold til kode. Så hvis vi tager RPS ud af Flasks ligning og får en anden service til at håndtere dem kan man forhindre denne bottleneck i applikationen. Her er [NGINX](https://www.nginx.com/blog/testing-the-performance-of-nginx-and-nginx-plus-web-servers/) et passende værktøj, da det kan håndtere mange flere RPS.

#### Hvad er fordelen ved NGINX?
NGINX kan fungere som en Webserver, Reverse proxy & som en load balancer til flere servere eller services. Ved at bruge NGINX som en reverse proxy til Flask, håndterer den problemet med Flasks RPS. 
NGINX kan også håndtere mange concurrent connections, og sørger for at den belastning, ligger på applikationen ikke kun handler om at have god hardware.

![NGINX_reverse_proxy](/images/NGINX_RP.png)

[Source](https://www.nginx.com/blog/maximizing-python-performance-with-nginx-parti-web-serving-and-caching/) 

#### Hvornår vil man bruge NGINX?
Flask vil fint kunne køre en mindre applikation, men NGINX vil være essentiel når man overstiger det antal RPS som Flask kan håndtere. NGINX vil kunne frigøre Flask at skulle håndtere [SSL](https://www.fairssl.dk/da/ssl-information/what-is-an-ssl-certificate) forbindelse, som er den del, som sørger for en sikker forbindelse. Dette gør at Flask frit kan håndtere requested uden at skulle lave et sikkerhedstjek. Billedet nedenfor repræsenterer NGINX RPS under forskellige omstændigheder.

![NGINX_request_per_second](/images/NGINX_RPS.png)

[Source](https://www.nginx.com/blog/testing-the-performance-of-nginx-and-nginx-plus-web-servers/)

#### Hvad medfører denne løsning?
Vi valgte at bruge NGINX da vores lærer skulle køre en simulator op imod vores applikation. Her kunne vi se på det antal RPS som han ville sende, at Flask umuligt ville kunne håndtere dette alene. Derfor valgte vi at bruge NGINX som en reverse proxy oven på vores Flask applikation, som gjorde det muligt at kunne håndtere langt flere RPS som dermed opfyldte kravene til hans simulator.



[<-- Ressourcer](https://michael2750.github.io/Flask_on_NGINX/sources)

[<-- Billeder](https://github.com/michael2750/Flask_on_NGINX/tree/master/images)

[<-- Gihub](https://github.com/michael2750/Flask_on_NGINX)
