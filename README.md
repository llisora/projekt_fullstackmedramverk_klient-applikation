# projectvue

Repo för klient-applikationen för projektuppgift i kursen Fullstacks-utveckling med Ramverk. 

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Views
```sh
HomeView - startsida
```
```sh
InventoryView - sida som visar vilka produkter som finns i lager samt möjlighet att lägga till nya produkter/uppdatera och radera.
```
```sh
LoginView - sida för inlogg - användaren måste vara inloggad för att komma vidare här ifrån.
```
```sh
RegisterView - sida för att skapa nya användare.
```
```sh
UpdateView - sida för att uppdatera enskild produkt. 
```
### Components
```sh
AddProducts - komponent för att på InventoryView kunna lägga till nya produkter.
```
```sh
Header - komponent för Header med RouterLinks till undersidor och länk för att logga ut.
```
```sh
Product - sida för att skriva ut produkterna - dessa skrivs ut i ett article-element och har knapp för att radera samt uppdatera.
```
