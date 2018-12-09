## Flask applikation kørende på Nginx
Hvis du gør brug af Flask i en større applikation er der stor sandsynlighed for dette ikke er den bedste løsning, da Flask har sine begrænsninger i forhold til, at håndtere requests.
Flask kan blive et problem for virksomheder, hvis mængden af requests overstiger den mængde Flask er i stand til at håndtere, og dermed skaber en bottleneck i applikationen. En nem løsning ville være at implementere Nginx, så man derved kan undgå den bottleneck der er opstået.
Ved at implementere Nginx vil firmaet både spare problemer angående klager, pga. et langsomt response, men den vil samtidig også øge applikationens stabilitet.

#### Hvem bruger flask?
Flask er begyndt at blive meget udbredt inden for softwareudvikling, men dens funktion til at skalere i forhold requests per second(RPS) er i den lave ende af de tilgængelige værktøjer, som er på markedet.
Flask er open source og kan implementeres hurtigt, dette gør det attraktivt at bruge til applikationer. Flask bliver brugt af dem, som skal sætte en simpel web application op og skal bruge en form for routing uden at skulle implementere et tykt interface. Flask giver en god learning experience, da det har ‘bare minimum’ i sig, og det derfor giver en større udfordring for udvikleren som øger erfaring inden for programmering.

#### Hvad er flask i stand til?
Flask er et micro-framework, hvilket betyder at den ikke har en masse ekstra værktøjer den propper i hovedet på dig som den mener du samtidig skal bruge.
Med Flask kan du derimod selv bygge meget af din applikation med en masse forskellige værktøjer/extensions som du foretrækker. Samtidig er Flask meget brugervenligt hvilket medfører til at dette betyder at du har meget større fleksibilitet i brugen af værktøjet. 

#### Hvilke ulemper har flask?
[Mark Hildreth](https://stackoverflow.com/questions/20843486/what-are-the-limitations-of-the-flask-built-in-web-server?answertab=votes#tab-top) Kommer ind på en af de svage punkter, som kommer med Flask. Frameworket er som udgangspunkt single threaded, altså vil Flask kun kunne håndtere et request ad gangen. Hvis et request rammer en bottleneck i applikationen, som tager f.eks 3 sekunder for at få et response, vil applikationen være sat i stå i mellemtiden. Flask kan køre multithreading, men det er stadig ikke tilstrækkeligt for applikation under ‘heavy load’.

#### Hvad er løsningen til dette problem?
Det gode ved Flask er at det skalere godt i forhold til kode. Så hvis vi tager RPS ud af Flasks ligning og får en anden service til at håndtere dem kan man forhindre denne bottleneck i applikationen. Her er [NGINX](https://www.nginx.com/blog/testing-the-performance-of-nginx-and-nginx-plus-web-servers/) et pragtfuldt eksempel da det kan håndtere mange flere RPS


[<-- Ressourcer](https://michael2750.github.io/Flask_on_NGINX/sources)

[<-- Billeder](https://github.com/michael2750/Flask_on_NGINX/tree/master/images)

[<-- Gihub](https://github.com/michael2750/Flask_on_NGINX)
